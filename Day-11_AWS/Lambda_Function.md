<img width="1204" height="301" alt="image" src="https://github.com/user-attachments/assets/97086d03-b1fd-4b2c-a00d-b02c3f4dbce3" />## Task – Automate Deletion of Unused EBS Snapshots with AWS Lambda

Description: -AWS Lambda is a serverless compute service that lets you run code without managing servers.
You just write your function code, set a trigger (like S3, CloudWatch, EventBridge, API Gateway, etc.), and AWS runs it automatically — only when needed.

## Create a Lambda function that:
- Lists all EBS snapshots owned by your account.
- Identifies old or unused snapshots (e.g., older than 7 or 30 days).
- Deletes those snapshots automatically.
- Logs all actions to CloudWatch Logs for auditing.

## Created snapshot
- Created snapshot to delete it from lambda
<img width="1226" height="406" alt="image" src="https://github.com/user-attachments/assets/bcf51301-bbeb-440d-95ba-5efe629ee4af" />

- Updated the python code in function and run the test but its failed due to permission issue
<img width="1215" height="817" alt="image" src="https://github.com/user-attachments/assets/01d05a06-7088-4ce8-9dc7-ba1fd687a067" />

- Created a policy and attached to the role
<img width="1224" height="805" alt="image" src="https://github.com/user-attachments/assets/9a43bcec-c1d2-4d60-babb-a3dfe65c68cd" />

- But need to add the decribe instance permission also hence added the same
<img width="1214" height="427" alt="image" src="https://github.com/user-attachments/assets/40045166-cfc8-4d24-923f-0111f828b576" />
<img width="1228" height="517" alt="image" src="https://github.com/user-attachments/assets/5692b1ba-9158-4844-91a8-561f613f854f" />

- Execution successfull, but snapshot was not delete, becuase the the volume and the instance is active
<img width="1206" height="811" alt="image" src="https://github.com/user-attachments/assets/ff9bc475-2a14-41eb-b475-1f29844dee25" />

- Created a test instance and creat snahot from it and terminated the instance
<img width="1223" height="473" alt="image" src="https://github.com/user-attachments/assets/229088c0-ccf2-4b51-a038-e7ed6f4e809e" />
<img width="1204" height="301" alt="image" src="https://github.com/user-attachments/assets/2d387c2b-0670-403c-b3a5-1c74734879d8" />

- Still the snapshot was not getting deleted, hence made some changes in code.
<img width="1201" height="631" alt="image" src="https://github.com/user-attachments/assets/d94d3354-ba7e-449f-ac86-4430a3f8913b" />

- Got permission issue again hence added decrivevolume permission for lambda role
<img width="1201" height="631" alt="image" src="https://github.com/user-attachments/assets/8329a901-01bb-42a7-b493-2720f36e8a42" />

- Deleted the unsed snapshots
<img width="1204" height="814" alt="image" src="https://github.com/user-attachments/assets/4fcdfe43-0ee0-4b7e-8eef-64375dccf0da" />

```
import boto3
import logging

# Configure logging
logger = logging.getLogger()
logger.setLevel(logging.INFO)

def lambda_handler(event, context):
    ec2 = boto3.client('ec2')

    # Dry run toggle — set to False when you're confident
    dry_run = True  

    # Get all EBS snapshots owned by the account
    snapshots = ec2.describe_snapshots(OwnerIds=['self'])['Snapshots']
    logger.info(f"Found {len(snapshots)} snapshots in your account.")

    # Get all active EC2 instance IDs
    instances_response = ec2.describe_instances(
        Filters=[{'Name': 'instance-state-name', 'Values': ['running']}]
    )

    active_instance_ids = {
        instance['InstanceId']
        for reservation in instances_response['Reservations']
        for instance in reservation['Instances']
    }

    logger.info(f"Active running instances: {active_instance_ids}")

    deleted_count = 0

    for snapshot in snapshots:
        snapshot_id = snapshot['SnapshotId']
        volume_id = snapshot.get('VolumeId')

        if not volume_id:
            # Delete the snapshot if it’s not associated with any volume
            try:
                if not dry_run:
                    ec2.delete_snapshot(SnapshotId=snapshot_id)
                logger.info(f"✅ Deleted snapshot {snapshot_id} (no volume attached).")
                deleted_count += 1
            except Exception as e:
                logger.error(f"❌ Failed to delete {snapshot_id}: {e}")
            continue

        # Check if the volume still exists
        try:
            volume_response = ec2.describe_volumes(VolumeIds=[volume_id])
            volume = volume_response['Volumes'][0]

            # If volume has no active attachments
            if not volume['Attachments']:
                if not dry_run:
                    ec2.delete_snapshot(SnapshotId=snapshot_id)
                logger.info(f"✅ Deleted snapshot {snapshot_id} (volume not attached to any instance).")
                deleted_count += 1

        except ec2.exceptions.ClientError as e:
            if e.response['Error']['Code'] == 'InvalidVolume.NotFound':
                # Volume deleted, snapshot orphaned
                try:
                    if not dry_run:
                        ec2.delete_snapshot(SnapshotId=snapshot_id)
                    logger.info(f"✅ Deleted snapshot {snapshot_id} (orphaned volume).")
                    deleted_count += 1
                except Exception as delete_err:
                    logger.error(f"❌ Failed to delete orphaned snapshot {snapshot_id}: {delete_err}")
            else:
                logger.error(f"⚠️ Error checking snapshot {snapshot_id}: {e}")

    logger.info(f"🎯 Completed cleanup — {deleted_count} snapshots deleted.")
```

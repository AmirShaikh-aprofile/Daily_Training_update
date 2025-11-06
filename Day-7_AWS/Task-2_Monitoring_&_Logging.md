# Task-2: Monitoring & Logging (CloudWatch, CloudTrail, SNS Alerts)

## 1. Create an SNS Topic 
- Create an SNS Topic with default setting(for Alerts)SNS Notifications
<img width="1867" height="789" alt="image" src="https://github.com/user-attachments/assets/ba07746b-8891-430d-8a14-da4efd18635f" />

- Created subscription and confirmed from email
<img width="1866" height="872" alt="image" src="https://github.com/user-attachments/assets/14492d5e-9cfe-4f03-949f-9821a08fb746" />


----
## 2. Create CloudWatch Alarm for EC2 Instance in ASG
**Monitor CPU utilization and send alert via SNS when above threshold**
- Created Alarm for CPU utilization after crossing 50% threshold based of ASG instance.
<img width="1852" height="864" alt="image" src="https://github.com/user-attachments/assets/7ef9999a-a540-42b7-986d-7a82c0891e20" />

- Tested the alarm by installing stress package in instance. Received email
<img width="1716" height="845" alt="image" src="https://github.com/user-attachments/assets/2225c1e7-750a-4489-aa87-57d9756dea08" />
<img width="1842" height="803" alt="image" src="https://github.com/user-attachments/assets/adc7d028-4f69-45ae-a0f8-2a923712c522" />

---
## 3. Enable Detailed Monitoring (Optional)
** To get 1-minute interval metrics instead of 5 minutes *
<img width="1861" height="836" alt="image" src="https://github.com/user-attachments/assets/deaa9357-4121-4e0f-9c9b-570852e6434f" />

---
## 4. Enabeling CloudTrail for Auditing
**To track all API calls, IAM changes, and console actions.**
- Created trail
<img width="1857" height="623" alt="image" src="https://github.com/user-attachments/assets/f216a098-f4fb-4a3b-93be-b7815b9e1031" />

- Able to see the cloudtrail logs in S3 bucket
<img width="1858" height="803" alt="image" src="https://github.com/user-attachments/assets/2b47ddf5-1ab9-40a6-9c9e-e4af125296b8" />

---

## 5. Configured CloudWatch Logs for Your Application (EC2)
**To send web/app logs from EC2 to CloudWatch for centralized monitoring.**
- After below troubleshooting
- Confirmed https service was running
<img width="684" height="335" alt="image" src="https://github.com/user-attachments/assets/988b77c2-3ae5-437d-b5d5-d841df10cadd" />

- Cloudwatch agent is runnig now
<img width="688" height="332" alt="image" src="https://github.com/user-attachments/assets/5da364ca-3b29-4cdb-a76f-e7f3835dc56c" />


----
## 4. Troubleshooting & Issues Faced
## Issue 1: Unable to start the cloudwatch-agent in the instance.
- Installed the agent in the instance and configured the agent to collect the metrics and logs but service was inactive after multiple troubleshoot.
-  Later found that the https service was running on the server but there is no log access logs on this path '/var/log/httpd/access_log'

- 'cwagent-config.json' file was not getting created after wizard setup.
- Hence created it manually.
```
sudo vim /opt/aws/amazon-cloudwatch-agent/etc/amazon-cloudwatch-agent.d/cwagent-config.json

sudo vim /opt/aws/amazon-cloudwatch-agent/etc/amazon-cloudwatch-agent.d/cwagent-config.json

```
```
{
  "agent": {
    "metrics_collection_interval": 60,
    "logfile": "/opt/aws/amazon-cloudwatch-agent/logs/amazon-cloudwatch-agent.log"
  },
  "metrics": {
    "append_dimensions": {
      "InstanceId": "${aws:InstanceId}"
    },
    "metrics_collected": {
      "cpu": {
        "measurement": ["usage_system", "usage_user", "usage_idle"]
      },
      "mem": {
        "measurement": ["mem_used_percent"]
      },
      "disk": {
        "measurement": ["used_percent"],
        "resources": ["*"]
      }
    }
  },
  "logs": {
    "logs_collected": {
      "files": {
        "collect_list": [
          {
            "file_path": "/var/log/httpd/access_log",
            "log_group_name": "/project/app/logs",
            "log_stream_name": "{instance_id}"
          }
        ]
      }
    }
  }
}

```



## Issue 2: Logs were not reflecting in cloudwatch aws console.
- After troubleshooting, found that the Ec2 instance dont have permission to send logs to cloudwatch
<img width="665" height="312" alt="image" src="https://github.com/user-attachments/assets/5e04c2b0-4493-4a2a-bfb3-728bc90b6bcc" />

- Solution:- Need to created IAM role and attched to EC2 to with required permission.  

- Created new role and attached to the instance
<img width="1863" height="718" alt="image" src="https://github.com/user-attachments/assets/bc4a3c18-d7fb-4be0-950b-e7b8a2ac124e" />

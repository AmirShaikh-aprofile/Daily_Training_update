# AMI_&_AWS_Backup -Automated backups for AWS services
## 1. Create AMi from aproject_web server with httpd service, cloudwatch agent installation, and app los in S3
<img width="1869" height="541" alt="image" src="https://github.com/user-attachments/assets/c65eb6ac-fffe-4a29-b0be-0a6ea9764dff" />

- Modified the lauch templete by adding the AMI in it and removing user data.
<img width="1864" height="815" alt="image" src="https://github.com/user-attachments/assets/57eb9e76-b127-4d57-a679-eb3f638787ca" />

- Update the new version in ASG
<img width="1849" height="844" alt="image" src="https://github.com/user-attachments/assets/f9e4ba31-0815-489d-810d-49ac3cb0146a" />

- Changed the desired count to confirm the changes
- New servers are launched but cloudwatch service is not 

## 2. EC2 (via EBS Snapshots / Lifecycle Manager)

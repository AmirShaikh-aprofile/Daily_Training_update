# S3_Integration via S3 VPC Endpoint:
Once created, AWS automatically routes S3 traffic internally (no internet needed)
# 1. Created Endpoint and added rout tables in it
<img width="1868" height="764" alt="image" src="https://github.com/user-attachments/assets/794f8bf0-10e5-4ed6-bdbf-7ed1babc7b01" />

- Policy: Choose “Full Access” for now
<img width="1607" height="697" alt="image" src="https://github.com/user-attachments/assets/3694b9ff-35fb-4948-979d-ac146f0326e6" />

---

# 2. Connect to EC2 (private instance) via jump server
- Try to list all the s3 bucket in account but due to permission issue, unable to list.
<img width="689" height="145" alt="image" src="https://github.com/user-attachments/assets/841e3bee-16e1-48b6-9aec-9dd31854c1c9" />

- Given S3 full access for testing purpose, Later, need to replace it with a least-privilege version:
<img width="573" height="84" alt="image" src="https://github.com/user-attachments/assets/309bd82f-3941-4755-b723-aed59a32b9df" />

---
# 3. Sending CloudWatch or App Logs to S3
**Option 1: Export CloudWatch Logs to S3 (Recommended for backups)**
<img width="1849" height="886" alt="image" src="https://github.com/user-attachments/assets/0dc09080-2981-40c7-b4cf-1e6de43a93d8" />


**Configure CloudWatch Agent → directly push logs to S3**
<img width="792" height="411" alt="image" src="https://github.com/user-attachments/assets/2de5bbf4-7fc5-46c8-be85-413b9971b91c" />


**Kinesis Firehose → S3- Unable to do it because of permission issue**
<img width="1846" height="878" alt="image" src="https://github.com/user-attachments/assets/718261f6-c31b-40fd-a430-d97693d98052" />

**Sending App Logs Directly to S3**
<img width="1084" height="221" alt="image" src="https://github.com/user-attachments/assets/dd1b5c2f-9b92-42a3-9b40-440b115183d7" />
<img width="1841" height="883" alt="image" src="https://github.com/user-attachments/assets/319038c2-4402-4bbe-a8c4-021de7d52c26" />

**Issue Faced:- Not getting logs in S3 bucket**
- Checked the cronjob configuration and it was lokking fine
- Checked the IAM pemirrions, the permission wasl also looks good
- Run the comand manually and found below error. Hence corrected the command and now the logs are uploding tin S3 bucket.
<img width="904" height="197" alt="image" src="https://github.com/user-attachments/assets/6c754195-4ffe-430f-903b-be3d8202c2ed" />
<img width="1844" height="871" alt="image" src="https://github.com/user-attachments/assets/959b5b45-6abc-4dd3-b259-2ca7458d4912" />

---

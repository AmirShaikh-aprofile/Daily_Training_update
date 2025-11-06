# Task2 - Storage & Database Layer

## 1. Created S3 Bucket Setup for Application Logs and Backups

**Steps Performed:**
- Created an S3 bucket to store web application logs and periodic backups.

![S3 Bucket Created](https://github.com/user-attachments/assets/0ea37b24-96e5-47d5-b7c6-5a7a9eb5d3e0)

**Lifecycle Policy Configured:**
- Transition **current versions** to **Glacier Flexible Retrieval** after **30 days**
- **Expire delete markers** after **180 days**

![Lifecycle Rule](https://github.com/user-attachments/assets/ddf9c771-3a93-4c90-b88e-c4ce7007ed30)
![Lifecycle Rule Details](https://github.com/user-attachments/assets/08f0b43e-2d1a-4fc7-a9c6-41fdba4f0900)

---

## 2. Hosted Application Database (MySQL) using Amazon RDS

**Configuration Details:**
- **Engine:** MySQL  
- **Version:** Default  
- **Master Username:** admin  
- **Password:** Stored securely in AWS Secrets Manager  

![RDS Config](https://github.com/user-attachments/assets/edbdd2ff-a128-48f3-8a23-e8c643060666)

**Connectivity Settings:**
- **VPC:** ProjectVPC  
- **Public Access:** Disabled  
- **Security Group:** Allow MySQL (3306) from EC2 Private SG  
- **Storage:** 20 GB gp3  
- **Backup Retention:** 7 days  

![RDS Connectivity](https://github.com/user-attachments/assets/c16cd9e4-f561-4cfb-9e32-dd31f56b1354)
![RDS Setup](https://github.com/user-attachments/assets/6e131251-f882-4dd1-8d59-22227b1170ae)

---

## 3. Verification

**Result:**  
Successfully connected to the RDS MySQL database from the EC2 instance.

![RDS Access from EC2](https://github.com/user-attachments/assets/da308e98-47af-490a-9614-24b8acc5caae)
<img width="685" height="117" alt="image" src="https://github.com/user-attachments/assets/1aca4811-7701-44f4-87a4-8a703a2a73fb" />

---

## 4. Troubleshooting & Issues Faced

### Issue 1: MySQL Command Not Found on EC2
![MySQL Error](https://github.com/user-attachments/assets/93f950a2-f327-47d1-94a3-b8f61fae8c9a)

**Description:**  
Encountered an error: `mysql: command not found` — because MySQL client was not installed on the EC2 instance.

**Resolution:**  
Installed the MySQL client package using:
```bash
sudo yum install mysql -y

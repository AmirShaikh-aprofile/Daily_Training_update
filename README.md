# 🚀 AWS CloudOps Hands-On Project

This repository documents my practical AWS CloudOps journey — aligned with the **AWS Certified Solutions Architect – Associate (SAA-C03)** and **AWS Certified CloudOps Associate** learning paths.

Over 6 days, I implemented and tested key AWS infrastructure components focusing on networking, compute, IAM, storage, monitoring, automation, and backup — following best practices and Infrastructure-as-Code principles.

---

## 📅 Project Overview

| Day | Focus Area | Key Deliverables |
|-----|-------------|------------------|
| **Day 1** | VPC & IAM Setup | Custom VPC with subnets, routing, NAT, IGW, and IAM roles |
| **Day 2** | Storage & Database Layer | S3 bucket for logs + RDS MySQL in private subnet |
| **Day 3** | Monitoring & Logging | CloudWatch, CloudTrail, SNS alerts |
| **Day 4** | Compute & Scaling | EC2 setup, roles, security groups, load balancing |
| **Day 5** | S3 Integration | VPC endpoint + S3 logging integration |
| **Day 6** | Monitoring & Backup | EC2 detailed monitoring, CloudWatch alarms, AWS Backup |

---

## 🧩 Day 1 – VPC & IAM Setup

### VPC Configuration
- **Name:** `ProjectVPC`
- **CIDR Block:** `10.0.0.0/16`
- **Subnets:**  
  - 2 Public (for bastion / NAT gateway)  
  - 2 Private (for EC2 + RDS)  
- **Routing:**  
  - Public subnets → Internet Gateway  
  - Private subnets → NAT Gateway  
- **DNS Support:** Enabled  

### IAM Configuration
- Created **IAM users, groups, and roles**.
- Enforced **MFA** for console users.
- Created **cross-account role** for testing access.
- Configured **least privilege policies**.

📁 *Deliverables:*  
`day1-networking-iam.md` + `vpc-diagram.png`

---

## 💾 Day 2 – Storage & Database Layer

### S3 Setup
- Created an **S3 bucket** to store logs and backups.
- Configured **Lifecycle Policy:**
  - Transition to Glacier after 30 days  
  - Expire delete markers after 180 days  

### RDS Setup
- Engine: **MySQL**
- Network: Hosted in private subnet (ProjectVPC)
- Security Group: Allows access only from EC2 private SG
- Storage: 20 GB gp3  
- Backup Retention: 7 days  
- Secrets stored in **AWS Secrets Manager**

📁 *Deliverables:*  
`day2-storage-database.md`

---

## 🧠 Day 3 – Monitoring & Logging

### CloudWatch Agent
- Installed and configured **Amazon CloudWatch Agent** on EC2.
- Collected `/var/log/httpd/access_log` and system metrics.

### CloudTrail
- Enabled **CloudTrail** for API activity logging.
- Logs delivered to S3 bucket `aws-account-logs`.

### SNS Alerts
- Created **SNS topic** `infra-alerts`.
- Subscribed email for alert notifications.

📁 *Deliverables:*  
`day3-monitoring-logging.md`

---

## ⚙️ Day 4 – Compute & Scaling

- Launched EC2 instances in private subnet.
- Associated **IAM Role** for S3 and CloudWatch access.
- Configured **Security Groups** for restricted inbound rules.
- Prepared setup for **Auto Scaling Group (ASG)** and **Application Load Balancer (ALB)** (optional step).

📁 *Deliverables:*  
`day4-compute-scaling.md`

---

## ☁️ Day 5 – S3 Integration

- Tested **S3 access from EC2** using:
  - **NAT Gateway** (for public access) or
  - **VPC Endpoint** (for private connectivity)
- Verified upload/download access with `aws s3 cp` commands.
- Configured **CloudWatch logs** to store in S3 bucket.

📁 *Deliverables:*  
`day5-s3-integration.md`

---

## 🧯 Day 6 – Monitoring & Backup

### CloudWatch Monitoring
- Enabled **Detailed Monitoring** on EC2 (1-minute metrics).
- Created **CloudWatch alarms** for:
  - CPUUtilization > 80%
  - StatusCheckFailed
  - Disk Usage
- Configured SNS notifications for alerts.

### AWS Backup
- Created **AWS Backup Plan** `ec2-backup-plan`
  - Daily backup schedule
  - Retention: 7 days
  - Resources: EC2 and EBS volumes
- RDS automated backups enabled.
- S3 lifecycle rule to transition to Glacier.

📁 *Deliverables:*  
`day6-monitoring-backup.md`

---

## 🧩 Tools & Services Used

| Category | Services |
|-----------|-----------|
| **Compute** | EC2, Auto Scaling |
| **Networking** | VPC, Subnets, NAT, IGW, Route Tables |
| **Storage** | S3, Glacier |
| **Database** | RDS (MySQL) |
| **Security** | IAM, MFA, Secrets Manager |
| **Monitoring** | CloudWatch, CloudTrail, SNS |
| **Backup** | AWS Backup |
| **Management** | AWS Console, CLI, IAM Roles |

---

## ✅ Validation Checklist

- [x] Custom VPC and networking setup  
- [x] IAM users, roles, MFA enforced  
- [x] S3 bucket + lifecycle policies  
- [x] RDS database functional  
- [x] CloudWatch logs integrated  
- [x] S3 endpoint tested from EC2  
- [x] Monitoring and backup plans configured  

---

## 📘 Learning Outcomes

- Designed and implemented **secure, scalable AWS infrastructure**.  
- Practiced **monitoring, logging, and automation**.  
- Configured **backups, alerts, and lifecycle management**.  
- Strengthened understanding of **AWS networking and IAM** fundamentals.

---

## 📎 Repository Structure


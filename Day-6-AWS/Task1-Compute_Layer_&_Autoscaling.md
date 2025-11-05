# Task1 - Compute Layer & Autoscaling

## 1. Created 2 Security Groups for Webserver and ALB

### Load Balancer Security Group
- **Inbound:** Allow HTTP (port 80) from `0.0.0.0/0`
- **Outbound:** Allow all

![Load Balancer SG](https://github.com/user-attachments/assets/09d63c7e-55c8-45a1-a70b-4526706ec03f)

### EC2 Instance Security Group
- **Inbound:** Allow HTTP (80) only from the Load Balancer SG
- **Outbound:** Allow all

---

## 2. Created a Launch Template with User Data (Bootstrapping Script)
```
Name: AProjectWebServerTemplate
AMI: Amazon Linux 3
Instance Type: t2.micro (Free tier)
Key Pair: (select one for SSH access)
Security Group: EC2 security group created earlier
User Data: Paste your bootstrap script here
```


![Launch Template 1](https://github.com/user-attachments/assets/70d5f2aa-d4d5-4d08-813f-12b6aeab51ee)
![Launch Template 2](https://github.com/user-attachments/assets/4a50e018-1b65-4412-aa94-86b2c1173a95)

---

## 3. Created an Application Load Balancer (ALB)

- Created a Target Group (TG) and attached it to the ALB.
- Verified listener configuration for HTTP (port 80).

![Target Group](https://github.com/user-attachments/assets/e8bccd5f-9c9b-4241-97c7-c37bf1a67da2)

- Created the ALB using two public subnets across different Availability Zones.

![ALB Created](https://github.com/user-attachments/assets/dd228898-a734-4b17-8404-cfc3fa6853e2)

---

## 4. Created Auto Scaling Group (ASG)

- Selected the Launch Template created earlier.  
- Chose the target VPC and **two private subnets** (for internal EC2s).

![ASG Subnets](https://github.com/user-attachments/assets/bd070981-83d9-4af5-a3b7-93b300081cef)

- Attached to existing Target Group (`AProject-TG`).

![ASG TG](https://github.com/user-attachments/assets/79b13dc9-b8da-4eee-8a74-286c3c97a93c)

- Used default scaling policy for initial testing.

![ASG Policy](https://github.com/user-attachments/assets/84451bfb-45e0-4abc-a7fe-f236dbb03ddd)

- Observed issue: Instances were **healthy in ASG but unhealthy behind the Target Group (TG)**.

![ASG Issue](https://github.com/user-attachments/assets/0632d12f-38cf-41c7-9249-311212531fac)

---

## 5. Issue Fixed — Web Server Accessible via ALB DNS

After troubleshooting, verified that the ALB DNS successfully routes traffic to healthy backend instances.

![ALB DNS Access](https://github.com/user-attachments/assets/808560ff-bcea-4a7d-b681-35708a9406c0)

---

# Troubleshooting

## Issue 1 — Instances Not Launching in ASG

### Observation
Instances were not launching in the Auto Scaling Group.  
Checked **ASG Activity Logs** and found the following error:

![ASG Error](https://github.com/user-attachments/assets/e3ef8017-e72f-45a7-b4cf-9f8a103218e3)

### Action Taken
Created a **new version** of the Launch Template by removing the **Spot Instance** configuration.  
Updated the ASG to use the new template version.

![Fixed Launch Template](https://github.com/user-attachments/assets/5bdb8d92-4f8a-4f4e-9835-21a1af35b4b3)

---

## Issue 2 — Instances Healthy in ASG but Unhealthy in TG

### Observation
Instances were showing as healthy in the ASG but **unhealthy behind the Target Group**.

![TG Unhealthy 1](https://github.com/user-attachments/assets/17654692-8006-41b4-a949-2855f875e762)
![TG Unhealthy 2](https://github.com/user-attachments/assets/2339cf25-7b51-454c-8e0b-5a65cb4eed2a)

### Root Cause
The **ALB Security Group** was not added in the **Web Server SG inbound rule**.

### Action Taken
Added the ALB SG in the web server’s SG inbound rule to allow traffic from the ALB.

![Fixed SG](https://github.com/user-attachments/assets/6f4fcdca-f148-4b32-8307-788b6421d9a0)
![TG Healthy](https://github.com/user-attachments/assets/e1774bea-9dc2-4a84-b5c2-7ad7c2677d1a)

---

## ✅ Summary

- Configured Security Groups for ALB and EC2.
- Built Launch Template with User Data script.
- Deployed Application Load Balancer and Target Group.
- Created Auto Scaling Group across private subnets.
- Troubleshot and resolved ASG/TG health issues.
- Verified web access via ALB DNS successfully.

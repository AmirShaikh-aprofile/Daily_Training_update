# Task-1 – Cross-Account S3 Access Setup

This document outlines the steps to configure **cross-account S3 access** between two AWS accounts:

## Created Ec2 instance and S3 bucket with policy
- Account A:Hosts the EC2 instance (Source)
<img width="1895" height="858" alt="image" src="https://github.com/user-attachments/assets/eb856517-2f76-4d60-9eca-29c682b5d889" />

- Created S3 bucket
<img width="1223" height="491" alt="image" src="https://github.com/user-attachments/assets/c98fc96d-6ec2-4846-8aa1-dfbd26b6f792" />

- Added bucket policy for cross account access
<img width="1218" height="811" alt="image" src="https://github.com/user-attachments/assets/3d8ac427-0cd7-4ae4-b690-f8d58b327067" />

- Created IAM rol and with inline policy and atatched to EC2
<img width="1251" height="749" alt="image" src="https://github.com/user-attachments/assets/1b1394e2-c8b8-4372-8c39-ab7590821c68" />

- Created test file and uploaded in S3 nucket
<img width="872" height="466" alt="image" src="https://github.com/user-attachments/assets/a5585b05-7ee1-463c-af5a-a3bfc29afd03" />

- <img width="1219" height="592" alt="image" src="https://github.com/user-attachments/assets/1b045e9b-77d4-4050-8f95-ab26e2560ce1" />

---

## Architecture Overview

```text
[Account A]
   └── EC2 Instance
        └── IAM Role → Accesses → [Account B] S3 Bucket


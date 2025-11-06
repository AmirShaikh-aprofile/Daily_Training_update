

## Created S3 Bucket Setup to store application logs or backups.
- Created S3 bucket
<img width="1869" height="544" alt="image" src="https://github.com/user-attachments/assets/0ea37b24-96e5-47d5-b7c6-5a7a9eb5d3e0" />

- Created below lifecycle rule
Transition current versions to Glacier Flexible Retrieval after 30 days
Expire delete markers after 180 days

<img width="1867" height="663" alt="image" src="https://github.com/user-attachments/assets/ddf9c771-3a93-4c90-b88e-c4ce7007ed30" />
<img width="1819" height="781" alt="image" src="https://github.com/user-attachments/assets/08f0b43e-2d1a-4fc7-a9c6-41fdba4f0900" />


---

## 2.  Host an application database (MySQL/PostgreSQL).
- Create RDS Database with below configurations
Engine: MySQL
Version: Default
Master username: admin
Password: (store safely in secrect manager)
<img width="386" height="269" alt="image" src="https://github.com/user-attachments/assets/edbdd2ff-a128-48f3-8a23-e8c643060666" />

Connectivity:
VPC: ProjectVPC
Public access: No
Security group: Allow MySQL (3306) from EC2 private SG
Storage: 20GB gp3
Backup retention: 7 days

<img width="1867" height="872" alt="image" src="https://github.com/user-attachments/assets/c16cd9e4-f561-4cfb-9e32-dd31f56b1354" />
<img width="1512" height="481" alt="image" src="https://github.com/user-attachments/assets/6e131251-f882-4dd1-8d59-22227b1170ae" />


## Result:
- Able to access the RDS server from EC2
<img width="691" height="189" alt="image" src="https://github.com/user-attachments/assets/da308e98-47af-490a-9614-24b8acc5caae" />

----
## Issues faced while task
## 1. 
<img width="693" height="57" alt="image" src="https://github.com/user-attachments/assets/93f950a2-f327-47d1-94a3-b8f61fae8c9a" />
Description:-  Getting this error because the mysql is not installed on Ec2 instance

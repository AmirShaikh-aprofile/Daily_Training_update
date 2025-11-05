# Task-2-Access_via_jump server.md

```
VPC
├── Public Subnet 1 (jump server / bastion host)
├── Public Subnet 2
├── Private Subnet 1 (2nd EC2 instance)
├── Private Subnet 2
├── IGW → Public Subnets
└── NAT Gateway → Private Subnets access Internet if needed
```
# 1. Created Ec2 jump server on public sunet.
<img width="890" height="240" alt="image" src="https://github.com/user-attachments/assets/95702c77-2c7b-48ba-8fe3-ba4034894bf8" />

----
# 2. Created Ec2 backend instance in private subnet.
<img width="459" height="69" alt="image" src="https://github.com/user-attachments/assets/88c4303a-ce3c-40b1-ba97-1ab484d52e35" />

----

# 3. COnfigured SG for bothe the instance
- Allowed SSH from jump server to pricate Ec2 without any public access.
<img width="1801" height="889" alt="image" src="https://github.com/user-attachments/assets/050aad52-acdf-454a-bc18-5205881bd626" />

___
- Allowed SSH from my laptop to jump server
<img width="1856" height="895" alt="image" src="https://github.com/user-attachments/assets/dde67f0a-755e-44df-9b72-73784b60e404" />

----
- Attched elastic IP to jump server
<img width="1639" height="365" alt="image" src="https://github.com/user-attachments/assets/6e781e26-d4f6-40c1-873d-f6937ff357a3" />

----
- Copied the key pair from my laptop to jump server.
- Changed the file permission and now able to access.
<img width="642" height="285" alt="image" src="https://github.com/user-attachments/assets/59e209bd-adc5-4be5-b6d9-cd4b022176b6" />




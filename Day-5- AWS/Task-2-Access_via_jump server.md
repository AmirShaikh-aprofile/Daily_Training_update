# Task-2-Access_via_jump server.md

# 1. 


```
VPC
├── Public Subnet 1 (jump server / bastion host)
├── Public Subnet 2
├── Private Subnet 1 (2nd EC2 instance)
├── Private Subnet 2
├── IGW → Public Subnets
└── NAT Gateway → Private Subnets access Internet if needed
```

----
- Changed the file permission and now able to access
<img width="642" height="285" alt="image" src="https://github.com/user-attachments/assets/59e209bd-adc5-4be5-b6d9-cd4b022176b6" />




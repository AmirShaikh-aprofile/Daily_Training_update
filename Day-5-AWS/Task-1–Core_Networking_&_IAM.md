# Task-1–Core_Networking_&_IAM.md

## 1. Created the VPC and Subnets
- Created a new VPC
<img width="1869" height="754" alt="image" src="https://github.com/user-attachments/assets/a4aa0e9b-4f1d-49f3-b849-0f121c830c23" />

- Created 4 Subnets in 2AZs
<img width="1857" height="843" alt="image" src="https://github.com/user-attachments/assets/f12d0f32-8ac2-45d1-99a5-d1d6c529560d" />

-----
## 2. Internet Gateway and NAT Gateway
- Created and Attach IGW to VPC
Description: An Internet Gateway (IGW) is a VPC component that allows resources in public subnets to connect to the internet.
<img width="1847" height="624" alt="image" src="https://github.com/user-attachments/assets/b36eeb91-4f15-47cd-9ae4-a5bfd2812cd4" />


- Create NAT Gateway and attached to public subnet
Description: A NAT Gateway allows private subnets to access the internet (for updates, downloads, etc.) without exposing them to inbound traffic.
<img width="1864" height="643" alt="image" src="https://github.com/user-attachments/assets/063bee2c-ac15-4792-808b-644784bb23a5" />

Note:
EC2 in public subnets can access the internet directly.
EC2 in private subnets can reach the internet via NAT.

-----

## 3. Configured Route 53 Private Hosted Zone

- Created a Private Hosted Zone:
Description: setting up private DNS resolution so that resources inside your VPC (like EC2 or RDS) can resolve internal names like
<img width="1867" height="883" alt="image" src="https://github.com/user-attachments/assets/54e4a0de-a5d8-4230-b56f-bef43e3996ab" />

- Created 1 ec instance in same VPC in public subnet
Description: To check if the dns works correctly
<img width="1866" height="719" alt="image" src="https://github.com/user-attachments/assets/ad82eaf8-d8cd-45ab-8fc0-51190c34b6da" />

- Added record sets:
Description: This way, we can refer to internal resources by name instead of IP.
<img width="1854" height="861" alt="image" src="https://github.com/user-attachments/assets/06fd6298-f6fd-4236-af65-4edbf54c784d" />

- Verified the dns record working fine
<img width="580" height="144" alt="image" src="https://github.com/user-attachments/assets/4efdb56d-dc9e-4e0a-b7b0-eba1e318e101" />

----

## 4. IAM Users, Groups, Roles, and MFA

- Created Groups and Policies with readonly access
<img width="1869" height="735" alt="image" src="https://github.com/user-attachments/assets/b85c3666-fbac-47ac-8dbc-63ccd7ea566f" />

- Create Users and enable console access and added the the group
- <img width="1849" height="890" alt="image" src="https://github.com/user-attachments/assets/eabaae1b-2a84-4ad1-b7e6-da553c772e89" />

---


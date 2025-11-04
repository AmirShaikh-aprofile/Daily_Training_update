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


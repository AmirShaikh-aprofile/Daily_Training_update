# Transit_Gateway_&_VPC_Peering_Setup.md

## VPC Peering
**1. Created VPC in both the accuunt**

VPC-Account A - 10.1.0.0/16
VPC-Account B - 10.0.0.0/16

<img width="1265" height="767" alt="image" src="https://github.com/user-attachments/assets/9df9cf39-df6b-4696-a859-f32d0d3dd635" />
<img width="1275" height="907" alt="image" src="https://github.com/user-attachments/assets/5a617583-fc53-4cda-823c-747db5947dee" />

---
## 2. Created Peering connection from Account A and Account B
- Created Peering connection from Account B and send request to Account A
<img width="1245" height="745" alt="image" src="https://github.com/user-attachments/assets/6f38fc3e-0a42-4cf5-8272-03ffc7990a92" />

- Accepted connect from account
<img width="1222" height="299" alt="image" src="https://github.com/user-attachments/assets/4408b216-1f9b-4194-b547-db2e36c1ce52" />
<img width="1225" height="653" alt="image" src="https://github.com/user-attachments/assets/0507f188-8747-48b6-94cf-70f716a33abd" />

---
## 3.Updated the peering connection as target in private route tables
<img width="1227" height="629" alt="image" src="https://github.com/user-attachments/assets/3f5d431c-172e-4b94-9aab-b8c8b1ca8f4a" />


## 4. Created server in both the account with in peered VPC to check the connectivity
## Issue faced while connecting 
**Both the server was in private subnet**
- So unable to SSH from the laptop, hence 1 server created in public subnet the tried to ping the server of another account.

**Unable to ping the server in diffrent account**
- While debugging found the route table entry was not added in public subnet , hence added the same
<img width="1272" height="544" alt="image" src="https://github.com/user-attachments/assets/0b06606c-8321-48c8-9758-72fb62963c59" />

- Able to ping the server now
<img width="593" height="275" alt="image" src="https://github.com/user-attachments/assets/3da4e876-8129-4691-b727-0f7958574d40" />

--------------------------------------------------



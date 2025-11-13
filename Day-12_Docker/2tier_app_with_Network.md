# Docker_Network.md
- Created a test network bridge
<img width="692" height="297" alt="image" src="https://github.com/user-attachments/assets/d96a0fa7-e853-4d2e-adf6-306f560c437e" />

----
## Created 2-tier infra using network
- Downloaded code from internet
- Build and docker image
<img width="1043" height="657" alt="image" src="https://github.com/user-attachments/assets/a1e84791-083b-41eb-a0fe-b60396a8fac2" />

- As per the code need to set environment in container, hence tried to run the container with environment setup
- But the container got exited
<img width="1051" height="206" alt="image" src="https://github.com/user-attachments/assets/0f586bea-bac9-4040-8c38-dc8e9cd9df0a" />

- Checked the logs andfound that it require netwrok bridge to connect the mydql container
<img width="796" height="235" alt="image" src="https://github.com/user-attachments/assets/de78d6fe-7bef-4dc9-b179-7b62d459c84b" />

- Hence createtd network bridge and attached to the containers
<img width="802" height="156" alt="image" src="https://github.com/user-attachments/assets/ead7483b-fa2c-433b-ad43-d54617ab45e0" />

**Issue observed**
- When running the mysql container the environment was wrong, hence made the changes 
 <img width="1052" height="488" alt="image" src="https://github.com/user-attachments/assets/f6e7d05d-cf09-43a1-89f8-eaae4ef10b3c" />
<img width="1056" height="423" alt="image" src="https://github.com/user-attachments/assets/f9bcf70e-26ea-4828-bb58-de3c2d2223a8" />

- The app container was getting exited, henc troubleshoot found that the environment was misplaced
- MYSQL_DATABASE=devops :- Correct one
- Issue got resolved after changes , botht the containers are running
<img width="1052" height="319" alt="image" src="https://github.com/user-attachments/assets/40e44034-8b01-4ee1-818d-76f54dca615e" />

-------
## Netwrok inspect
- Changed the containers running in out network
<img width="1001" height="690" alt="image" src="https://github.com/user-attachments/assets/272612b2-bd53-4d03-aa1a-64062be9ef70" />

- Enabled port 5000 from the SG
<img width="1201" height="706" alt="image" src="https://github.com/user-attachments/assets/623361d3-f02a-46fc-8b29-67ce07573074" />

- Able to access the website from browser
<img width="1248" height="790" alt="image" src="https://github.com/user-attachments/assets/87b72080-cbaa-49fb-96ca-697ed42c92ff" />

- Added some messages from site
<img width="1118" height="717" alt="image" src="https://github.com/user-attachments/assets/d2a05d2b-0356-4daa-ab6a-5f22571bef52" />

- Confirmed the same from database
<img width="804" height="702" alt="image" src="https://github.com/user-attachments/assets/f8299875-4d50-4117-89fc-13fe27455485" />

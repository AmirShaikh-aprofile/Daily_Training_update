## Install_MDATP_&_AMI.md
**As per EIC policy need to install MDATP in all node**
- Incresed count and from ASG of current cluster
<img width="1214" height="816" alt="image" src="https://github.com/user-attachments/assets/8f70654f-ff27-4a94-b2e2-ebb74ef3e7c7" />

- Installed the MDATP on the instance
<img width="1388" height="771" alt="image" src="https://github.com/user-attachments/assets/b113ad2e-4a34-4da5-97d2-fbfebf1450cf" />

- Created AMI image of the instance after confirming from IT team.
<img width="1222" height="791" alt="image" src="https://github.com/user-attachments/assets/8c5adb4c-eb82-4f4f-a755-0739ae60091e" />

- Created NG with new AMI
```
eksctl create nodegroup --cluster=eksdemo2-amir \
    --region=ap-south-1 \
    --name=eksdemo-amir-ng-2-public1 \
    --node-type=t3.medium \
    --nodes=2 \
    --nodes-min=2 \
    --nodes-max=4 \
    --node-volume-size=20 \
    --ssh-access \
    --ssh-public-key=amir_key \
    --managed \
    --node-ami-family AmazonLinux2023 \
    --node-ami ami-039c2313054ae6ac9 \
    --asg-access \
    --external-dns-access \
    --full-ecr-access \
    --appmesh-access \
    --alb-ingress-access
```
<img width="1217" height="752" alt="image" src="https://github.com/user-attachments/assets/a433af3c-71c1-4e49-a301-9e091322c83e" />

- Confirm the MDAPT in running in new NG
<img width="1257" height="933" alt="image" src="https://github.com/user-attachments/assets/39a1d8e7-d18e-4e4c-baca-82c8f4feb111" />


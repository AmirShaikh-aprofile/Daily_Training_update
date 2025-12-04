# Installations_Prerequisite

1. Already have AWS account

2. Already have IAM user with required permissions.

3. Creating Ec2 instance for project implementation on locally.
- Created Ubuntu_24.04 Ec2 and installed Mdatp with t2.large
- <img width="1203" height="443" alt="image" src="https://github.com/user-attachments/assets/cb7e5862-71d8-4de5-9292-96cd7ba54606" />

4. Installing docker:
- Installed docker on instance.And added ubuntu user in docker group.```sudo usermod -aG docker ubuntu```
- https://docs.docker.com/engine/install/ubuntu/
- <img width="790" height="364" alt="image" src="https://github.com/user-attachments/assets/22df9d71-0c46-4c69-8a12-b2926a1f82da" />


5. Installing kubectl
- Installed Kubectl using below doc.
- https://kubernetes.io/docs/tasks/tools/install-kubectl-linux/
- <img width="793" height="78" alt="image" src="https://github.com/user-attachments/assets/03e02fd5-fcb9-4fe4-ab1e-1e3e9bf66dd6" />

6. Installing Terraform.
- Installed Terraform using below doc.
- https://developer.hashicorp.com/terraform/tutorials/aws-get-started/install-cli
- <img width="396" height="60" alt="image" src="https://github.com/user-attachments/assets/24437511-e7e4-40c5-aa6b-3f2a4dcdbb79" />

--------------

# Running Project locally on Ec2 instance.

1. Cloned the repo ```https://github.com/iam-veeramalla/ultimate-devops-project-demo.git```
2. While running project locally, getting below error, which means 'containerd mount leak during docker build'.
- Hence resoved the issue by unmount all stuck containerd tmpmounts.
- ```failed to unmount /var/lib/containerd/tmpmounts/... : device or resource busy```
- ```
sudo systemctl stop docker
sudo systemctl stop containerd
sudo umount -f /var/lib/containerd/tmpmounts/* 2>/dev/null
sudo rm -rf /var/lib/containerd/tmpmounts/*
sudo rm -rf /var/lib/docker/overlay2/*/merged
sudo systemctl start containerd
sudo systemctl start docker
docker builder prune -af
docker system prune -af --volumes
```

3. Wedsite is accesable from the public IP of my instance
- ```http://13.202.187.125:8080/```
- <img width="1265" height="965" alt="image" src="https://github.com/user-attachments/assets/aa01dfd7-89f7-49c5-8f09-896a48e0b578" />





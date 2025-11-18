## 1. Creating EKS Cluster using eksctl.
<img width="1855" height="855" alt="image" src="https://github.com/user-attachments/assets/00087c95-bf9d-4b4d-8c17-434b5ea787fb" /># Cluster_Creation.md

**Issue-1 faced while creating cluster via eksctl CLI**
- Observerd that the region was seleted wrong, issue resolved after changing the region.
<img width="662" height="500" alt="image" src="https://github.com/user-attachments/assets/c1c9883e-3445-46dd-8e20-f3ee8768865e" />

**Issue-2 Unable to create VPC anad elastic IP becuase of maximum limit
<img width="654" height="557" alt="image" src="https://github.com/user-attachments/assets/1561226d-655b-49d1-a8d6-b3aa056bb9a0" />
Solution:- Release an IP address from NAT gateway for unused account and created cluster in default VPC.

- Cluster got created without Nodegroup
<img width="1855" height="855" alt="image" src="https://github.com/user-attachments/assets/b5b0e077-8e78-46d2-9571-dba9aeb41cb2" />
<img width="574" height="57" alt="image" src="https://github.com/user-attachments/assets/fd1575da-b28d-463c-bb1a-cb59950808f7" />

---

## Step-02: Create & Associate IAM OIDC Provider for our EKS Cluster
- To enable and use AWS IAM roles for Kubernetes service accounts on our EKS cluster, we must create &  associate OIDC identity provider.
- To do so using `eksctl` we can use the  below command. 
- Use latest eksctl version (as on today the latest version is `0.21.0`)
```                   
# Replace with region & cluster name
eksctl utils associate-iam-oidc-provider \
    --region ap-south-1 \
    --cluster eksdemo2-amir \
    --approve
```

---
## Step-03: Create EC2 Keypair
- Using existing keypair
<img width="650" height="160" alt="image" src="https://github.com/user-attachments/assets/521fe83d-29d5-4d6f-b46d-2553a5596fe3" />

---
## Step-04: Create Node Group with additional Add-Ons in Public Subnets
- These add-ons will create the respective IAM policies for us automatically within our Node Group role.
 ```
# Create Public Node Group   
eksctl create nodegroup --cluster=eksdemo2-amir \
                        --region=ap-south-1 \
                        --name=eksdemo2-amir-ng-public1 \
                        --node-type=t3.medium \
                        --nodes=2 \
                        --nodes-min=2 \
                        --nodes-max=4 \
                        --node-volume-size=20 \
                        --ssh-access \
                        --ssh-public-key=amir_key \
                        --managed \
                        --asg-access \
                        --external-dns-access \
                        --full-ecr-access \
                        --appmesh-access \
                        --alb-ingress-access 
```
<img width="654" height="572" alt="image" src="https://github.com/user-attachments/assets/2297edd3-6fbe-4c02-a583-130bec4444b6" />

----
## Step-05: Verify Cluster & Nodes

### Verify NodeGroup subnets to confirm EC2 Instances are in Public Subnet
- Verify the node group subnet to ensure it created in public subnets
  - Go to Services -> EKS -> eksdemo -> eksdemo2-amir-ng1-public
  - Click on Associated subnet in **Details** tab
  - Click on **Route Table** Tab.
  - We should see that internet route via Internet Gateway (0.0.0.0/0 -> igw-xxxxxxxx)

### Verify Cluster, NodeGroup in EKS Management Console
- Go to Services -> Elastic Kubernetes Service -> eksdemo2-amir

### List Worker Nodes
```
# List EKS clusters
eksctl get cluster

# List NodeGroups in a cluster
eksctl get nodegroup --cluster=eksdemo2-amir

# List Nodes in current kubernetes cluster
kubectl get nodes -o wide

# Our kubectl context should be automatically changed to new cluster
kubectl config view --minify
```
- Verified- all the details are correct
<img width="654" height="203" alt="image" src="https://github.com/user-attachments/assets/23d635d9-8103-449b-b6cd-75e4df1a74d5" />

### Verify Worker Node IAM Role and list of Policies
- Go to Services -> EC2 -> Worker Nodes
- Click on **IAM Role associated to EC2 Worker Nodes**
<img width="1203" height="574" alt="image" src="https://github.com/user-attachments/assets/cf766ca9-467f-45ae-a477-59839cc072f5" />


### Verify Security Group Associated to Worker Nodes
- Go to Services -> EC2 -> Worker Nodes
- Click on **Security Group** associated to EC2 Instance which contains `remote` in the name.


### Verify CloudFormation Stacks
- Verify Control Plane Stack & Events
- Verify NodeGroup Stack & Events
<img width="1201" height="645" alt="image" src="https://github.com/user-attachments/assets/d733b47a-47cc-46f3-b001-35b32e0ff047" />

### Login to Worker Node using Keypair 'amir_key'
- Login to worker node
```
# For Linux or Windows10
ssh -i kube-demo.pem ec2-user@65.2.179.120

```
<img width="556" height="235" alt="image" src="https://github.com/user-attachments/assets/9c9e7f8e-041b-40a3-8076-34191eb7cf2d" />

## Step-06: Update Worker Nodes Security Group to allow all traffic
- We need to allow `All Traffic` on worker node security group
<img width="1217" height="781" alt="image" src="https://github.com/user-attachments/assets/c3da118d-df7e-4b0f-ac6c-7d24d56a3135" />
---



















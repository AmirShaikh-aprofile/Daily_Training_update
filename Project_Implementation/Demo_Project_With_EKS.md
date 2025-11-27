## Created cluster with farget profile using eksctl and kubectl.
<img width="1216" height="802" alt="image" src="https://github.com/user-attachments/assets/6d6e8e14-78b3-4b0b-b25e-74c4e8a0ecca" />

```
eksctl create fargateprofile \
    --cluster demo-cluster \
    --region us-east-1 \
    --name alb-sample-app \
    --namespace game-2048
```

-----------
## Deployed the pods

<img width="648" height="127" alt="image" src="https://github.com/user-attachments/assets/57c66a12-ad19-43f2-be9a-c71d0ffad494" />
```
kubectl apply -f https://raw.githubusercontent.com/kubernetes-sigs/aws-load-balancer-controller/v2.5.4/docs/examples/2048/2048_full.yaml
```

```
---
apiVersion: v1
kind: Namespace
metadata:
  name: game-2048
---
apiVersion: apps/v1
kind: Deployment
metadata:
  namespace: game-2048
  name: deployment-2048
spec:
  selector:
    matchLabels:
      app.kubernetes.io/name: app-2048
  replicas: 5
  template:
    metadata:
      labels:
        app.kubernetes.io/name: app-2048
    spec:
      containers:
      - image: public.ecr.aws/l6m2t8p7/docker-2048:latest
        imagePullPolicy: Always
        name: app-2048
        ports:
        - containerPort: 80
---
apiVersion: v1
kind: Service
metadata:
  namespace: game-2048
  name: service-2048
spec:
  ports:
    - port: 80
      targetPort: 80
      protocol: TCP
  type: NodePort
  selector:
    app.kubernetes.io/name: app-2048
---
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  namespace: game-2048
  name: ingress-2048
  annotations:
    alb.ingress.kubernetes.io/scheme: internet-facing
    alb.ingress.kubernetes.io/target-type: ip
spec:
  ingressClassName: alb
  rules:
    - http:
        paths:
        - path: /
          pathType: Prefix
          backend:
            service:
              name: service-2048
              port:
                number: 80
```

# How to setup alb add on

Download IAM policy

```
curl -O https://raw.githubusercontent.com/kubernetes-sigs/aws-load-balancer-controller/v2.11.0/docs/install/iam_policy.json
```

Create IAM Policy

```
aws iam create-policy \
    --policy-name AWSLoadBalancerControllerIAMPolicy \
    --policy-document file://iam_policy.json
```

Create IAM Role

```
eksctl create iamserviceaccount \
  --cluster=<your-cluster-name> \
  --namespace=kube-system \
  --name=aws-load-balancer-controller \
  --role-name AmazonEKSLoadBalancerControllerRole \
  --attach-policy-arn=arn:aws:iam::<your-aws-account-id>:policy/AWSLoadBalancerControllerIAMPolicy \
  --approve
```
<img width="746" height="187" alt="image" src="https://github.com/user-attachments/assets/8826c76b-0e04-4d40-8234-8a28ed4ad5e9" />

## Deploy ALB controller

Add helm repo

```
helm repo add eks https://aws.github.io/eks-charts
```

Update the repo

```
helm repo update eks
```
<img width="743" height="393" alt="image" src="https://github.com/user-attachments/assets/57436ba0-cff7-4f07-91a2-6b9d70751204" />

## Install

```
helm install aws-load-balancer-controller eks/aws-load-balancer-controller -n kube-system \
  --set clusterName=<your-cluster-name> \
  --set serviceAccount.create=false \
  --set serviceAccount.name=aws-load-balancer-controller \
  --set region=<your-region> \
  --set vpcId=<your-vpc-id>
```
<img width="746" height="244" alt="image" src="https://github.com/user-attachments/assets/cf13602f-1578-4747-a594-4e7a17053cda" />

Verify that the deployments are running.

```
kubectl get deployment -n kube-system aws-load-balancer-controller
```
## Pods are running after issue resolve
<img width="612" height="401" alt="image" src="https://github.com/user-attachments/assets/155a3136-2bd1-4368-a525-19ae8afccb8f" />



# Issue faced
## Controler pods were not getting up sue to service account issue.
Solution: override the service account 
<img width="719" height="374" alt="image" src="https://github.com/user-attachments/assets/4cb7b55d-801f-48b3-934c-bae15034a6de" />

- Hence overide the service account while creating again
<img width="741" height="324" alt="image" src="https://github.com/user-attachments/assets/9e069164-8aea-424a-90f7-21624bb64115" />

- Deleted older deployment
<img width="736" height="47" alt="image" src="https://github.com/user-attachments/assets/bdf5d898-8609-427d-a524-2874695f4956" />

- Create the al-controller again using helm
<img width="745" height="248" alt="image" src="https://github.com/user-attachments/assets/de2112b2-5025-4d6b-90fc-1fbea3de4768" />

- Obsevred the same issue, hence deleted the stack from CF and created new iamserviceaccount
- Pods are running state now
<img width="738" height="406" alt="image" src="https://github.com/user-attachments/assets/9c939e79-2302-4c61-ab93-b5f8a8f34415" />

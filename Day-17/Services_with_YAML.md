# Services with YAML

## Step-01: Introduction to Services
- We are going to look in to below two services in detail with a frotnend and backend example
  - NodePort Service
  - ClusterIP Service

## Step-02: Create Backend Deployment & Cluster IP Service
- Write the Deployment template for backend REST application.
- Write the Cluster IP service template for backend REST application.
- **Important Notes:** 
  - Name of Cluster IP service should be `name: my-backend-service` because  same is configured in frontend nginx reverse proxy `default.conf`. 
  - Test with different name and understand the issue we face
  - We have also discussed about in our section [05-Services-with-kubectl](/05-Services-with-kubectl/README.md)
```
cd <Course-Repo>\kubernetes-fundamentals\10-Services-with-YAML\kube-manifests
kubectl get all
kubectl apply -f 01-backend-deployment.yml -f 02-backend-clusterip-service.yml
kubectl get all
```
<img width="592" height="515" alt="image" src="https://github.com/user-attachments/assets/33142f52-72c7-43cb-8acd-1e0614d79987" />
<img width="590" height="590" alt="image" src="https://github.com/user-attachments/assets/58837653-abe5-4d1f-83fa-c072707336a8" />


## Step-03: Create Frontend Deployment & NodePort Service
- Write the Deployment template for frontend Nginx Application
- Write the NodePort service template for frontend Nginx Application
```
cd <Course-Repo>\kubernetes-fundamentals\10-Services-with-YAML\kube-manifests
kubectl get all
kubectl apply -f 03-frontend-deployment.yml -f 04-frontend-nodeport-service.yml
kubectl get all
```
- **Access REST Application**
```
# Get External IP of nodes using
kubectl get nodes -o wide

# Access REST Application  (Port is static 31234 configured in frontend service template)
http://<node1-public-ip>:31234/hello
```
<img width="830" height="309" alt="image" src="https://github.com/user-attachments/assets/8f219aa7-6c01-4da6-a3df-8cedea903072" />
<img width="665" height="237" alt="image" src="https://github.com/user-attachments/assets/e1130e11-5bb4-4696-92fe-ec74c4e11a33" />
<img width="547" height="185" alt="image" src="https://github.com/user-attachments/assets/656cc1ed-691a-45f8-bc16-26364c6ea46a" />

## Step-04: Delete & Recreate Objects using kubectl apply
### Delete Objects (file by file)
```
kubectl delete -f 01-backend-deployment.yml -f 02-backend-clusterip-service.yml -f 03-frontend-deployment.yml -f 04-frontend-nodeport-service.yml
kubectl get all
```
<img width="912" height="202" alt="image" src="https://github.com/user-attachments/assets/d08c18ce-3ed0-4c06-9f4a-d7c7a4a3511a" />

### Recreate Objects using YAML files in a folder
```
cd <Course-Repo>\kubernetes-fundamentals\10-Services-with-YAML
kubectl apply -f kube-manifests/
kubectl get all
```
<img width="881" height="599" alt="image" src="https://github.com/user-attachments/assets/acfaf846-d6bc-49c9-b0a8-0880639251b8" />

### Delete Objects using YAML files in folder
```
cd <Course-Repo>\kubernetes-fundamentals\10-Services-with-YAML
kubectl delete -f kube-manifests/
kubectl get all
```
- Before- <img width="902" height="458" alt="image" src="https://github.com/user-attachments/assets/a7f4ddb6-85cc-4c15-8246-0193479340a0" />
- After- <img width="757" height="230" alt="image" src="https://github.com/user-attachments/assets/3d1c8a9f-5154-4572-ad93-a78eb4e34f96" />



## Additional References - Use Label Selectors for get and delete
- https://kubernetes.io/docs/concepts/cluster-administration/manage-deployment/#using-labels-effectively
- https://kubernetes.io/docs/concepts/overview/working-with-objects/labels/#label-selectors

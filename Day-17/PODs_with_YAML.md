# PODs with YAML
## Step-01: Kubernetes YAML Top level Objects
- Discuss about the k8s YAML top level objects
- **01-kube-base-definition.yml**
```yml
apiVersion:
kind:
metadata:
  
spec:
```
-  **Pod API Objects Reference:**  https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.18/#pod-v1-core

## Step-02: Create Simple Pod Definition using YAML 
- We are going to create a very basic pod definition
- **02-pod-definition.yml**
```yml
apiVersion: v1 # String
kind: Pod  # String
metadata: # Dictionary
  name: myapp-pod
  labels: # Dictionary 
    app: myapp         
spec:
  containers: # List
    - name: myapp
      image: stacksimplify/kubenginx:1.0.0
      ports:
        - containerPort: 80
```
- **Create Pod**
```
# Create Pod
kubectl create -f 02-pod-definition.yml
[or]
kubectl apply -f 02-pod-definition.yml

# List Pods
kubectl get pods
```
<img width="574" height="193" alt="image" src="https://github.com/user-attachments/assets/f6e5add5-a144-49c8-b3e1-3c3945669ac1" />

## Step-03: Create a NodePort Service
- **03-pod-nodeport-service.yml**
```yml
apiVersion: v1
kind: Service
metadata:
  name: myapp-pod-nodeport-service  # Name of the Service
spec:
  type: NodePort
  selector:
  # Loadbalance traffic across Pods matching this label selector
    app: myapp
  # Accept traffic sent to port 80    
  ports: 
    - name: http
      port: 80    # Service Port
      targetPort: 80 # Container Port
      nodePort: 31231 # NodePort
```
- **Create NodePort Service for Pod**
```
# Create Service
kubectl apply -f 03-pod-nodeport-service.yml

# List Service
kubectl get svc

# Get Public IP
kubectl get nodes -o wide

# Access Application
http://<WorkerNode-Public-IP>:<NodePort>
http://<WorkerNode-Public-IP>:31231
```
<img width="575" height="242" alt="image" src="https://github.com/user-attachments/assets/0fac76e3-52df-435e-a04d-025783e6f3a8" />
<img width="645" height="281" alt="image" src="https://github.com/user-attachments/assets/ef65d991-af3e-4558-8189-59b63797cfc9" />

## API Object References
-  **Pod**: https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.18/#pod-v1-core
- **Service**: https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.18/#service-v1-core

## Updated API Object References
-  **Pod**: https://kubernetes.io/docs/reference/kubernetes-api/workload-resources/pod-v1/
-  **Service**: https://kubernetes.io/docs/reference/kubernetes-api/service-resources/service-v1/
- **Kubernetes API Reference:** https://kubernetes.io/docs/reference/kubernetes-api/

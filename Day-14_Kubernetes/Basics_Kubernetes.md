# 1. Introduction to Kubernetes

## What is Kubernetes?
Kubernetes (K8s) is an open-source container orchestration platform that automates:
- Deployment of containers  
- Scaling applications  
- Management of containerized workloads  
- Load balancing and service discovery  

## Why Kubernetes?
- Self-healing containers  
- Auto-scaling  
- Rolling updates and rollbacks  
- Infrastructure abstraction  
- Efficient resource usage  
- Declarative configuration  

---

# 2. Kubernetes Architecture

## Control Plane Components
| Component | Description |
|----------|-------------|
| **API Server** | Entry point for all cluster operations |
| **Etcd** | Distributed key-value store storing cluster state |
| **Scheduler** | Selects optimal nodes for pod placement |
| **Controller Manager** | Ensures desired cluster state |

## Worker Node Components
| Component | Description |
|----------|-------------|
| **Kubelet** | Communicates with control plane; runs pods |
| **Kube-proxy** | Manages networking rules |
| **Container Runtime** | Docker, containerd, CRI-O |
# 3. Key Kubernetes Concepts

## Pod
- Smallest deployable unit  
- Contains one or more containers  

## ReplicaSet
- Ensures a specific number of pod replicas

## Deployment
- Manages ReplicaSets and provides rolling updates  

## Service
Provides stable networking to pods.

### Service Types:
- ClusterIP  
- NodePort  
- LoadBalancer  
- ExternalName  

## Namespace
- Organizes cluster resources  

## ConfigMap
- Stores non-sensitive configuration data  

## Secret
- Stores sensitive data (Base64 encoded)  

## Ingress
- Routes HTTP/HTTPS traffic into the cluster  

---

# 4. Kubernetes YAML Examples

## Deployment YAML
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deploy
spec:
  replicas: 2
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
        - name: nginx
          image: nginx
          ports:
            - containerPort: 80
```
**Service YAML (NodePort)**
```
apiVersion: v1
kind: Service
metadata:
  name: nginx-service
spec:
  type: NodePort
  selector:
    app: nginx
  ports:
    - port: 80
      targetPort: 80
      nodePort: 30007
```

**ConfigMap YAML**
apiVersion: v1
kind: ConfigMap
metadata:
  name: app-config
data:
  APP_ENV: production
  LOG_LEVEL: info

**Secret YAML**
apiVersion: v1
kind: Secret
metadata:
  name: app-secret
type: Opaque
data:
  username: YWRtaW4=
  password: MTIzNDU2

**Ingress YAML**
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: example-ingress
spec:
  rules:
    - host: example.com
      http:
        paths:
          - path: /
            pathType: Prefix
            backend:
              service:
                name: nginx-service
                port:
                  number: 80

## 5. kubectl Commands
**Cluster Info**
kubectl version
kubectl cluster-info
kubectl get nodes

**Pods**
kubectl get pods
kubectl describe pod <pod-name>
kubectl logs <pod-name>
kubectl exec -it <pod-name> -- bash

**Deployments**
kubectl get deployments
kubectl describe deployment nginx-deploy

**Apply/Delete YAMLs**
kubectl apply -f file.yaml
kubectl delete -f file.yaml

**Services**
kubectl get svc
kubectl describe svc nginx-service

## 6. Kubernetes Networking
**Key Points**

Each pod gets its own IP

CNI plugins (Calico, Flannel, Weave) provide networking

Services provide stable networking

Ingress handles HTTP/HTTPS routes

**Service Types Summary**
**Type	Description**
ClusterIP	Internal access only
NodePort	Exposes service on each node
LoadBalancer	External access using LB
ExternalName	Maps service to external DNS

## 7. Kubernetes Storage
**Volume**

Temporary storage tied to pod lifecycle.

PersistentVolume (PV)

Cluster-level storage provider.

PersistentVolumeClaim (PVC)

A request for storage by a pod.

StorageClass

Defines types of storage (SSD/HDD).

**PVC Example**
```
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: mypvc
spec:
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 1Gi
  storageClassName: standard
```

## 8. Scaling in Kubernetes
Manual Scaling
kubectl scale deployment nginx-deploy --replicas=5

**Auto Scaling (HPA)**
apiVersion: autoscaling/v2
kind: HorizontalPodAutoscaler
metadata:
  name: nginx-hpa
spec:
  scaleTargetRef:
    apiVersion: apps/v1
    kind: Deployment
    name: nginx-deploy
  minReplicas: 2
  maxReplicas: 10
  metrics:
    - type: Resource
      resource:
        name: cpu
        target:
          type: Utilization
          averageUtilization: 70

## 9. Health Probes
**Liveness Probe**

Checks if the app is alive.

Readiness Probe

Checks if app is ready for traffic.

Example
```
livenessProbe:
  httpGet:
    path: /
    port: 80
  initialDelaySeconds: 5
  periodSeconds: 10

readinessProbe:
  httpGet:
    path: /
    port: 80
  initialDelaySeconds: 2
  periodSeconds: 5
```

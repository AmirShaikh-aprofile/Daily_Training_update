# 🚀 DevOps Command Cheat Sheet  
### Docker • Kubernetes • Terraform

---

# 📦 Docker — Essential Commands

## 🟦 Container Commands

| Command | Description |
|--------|-------------|
| `docker ps` | List running containers |
| `docker ps -a` | List all containers |
| `docker run <image>` | Run a container |
| `docker run -d <image>` | Run container in detached mode |
| `docker run -p 8080:80 <image>` | Map host port to container port |
| `docker stop <id>` | Stop a container |
| `docker start <id>` | Start a stopped container |
| `docker restart <id>` | Restart a container |
| `docker logs <id>` | View logs |
| `docker logs -f <id>` | Follow logs |
| `docker exec -it <id> bash` | Exec into a running container |

---

## 🟦 Image Commands

| Command | Description |
|--------|-------------|
| `docker images` | List images |
| `docker pull <image>` | Download image |
| `docker build -t name:tag .` | Build image from Dockerfile |
| `docker rmi <image>` | Remove image |
| `docker tag src:tag dest:tag` | Tag an image |
| `docker push repo/image:tag` | Push image to registry |

---

## 🟦 Cleanup Commands

| Command | Description |
|--------|-------------|
| `docker system prune` | Remove unused data |
| `docker system prune -af --volumes` | Aggressive cleanup |
| `docker builder prune` | Remove build cache |

---

# ☸️ Kubernetes (kubectl) — Essential Commands

## 🟩 Cluster & Context

| Command | Description |
|--------|-------------|
| `kubectl version --short` | Show client/server version |
| `kubectl cluster-info` | Cluster info |
| `kubectl config get-contexts` | List kubeconfig contexts |
| `kubectl config use-context <context>` | Switch context |

---

## 🟩 Pods

| Command | Description |
|--------|-------------|
| `kubectl get pods` | List pods |
| `kubectl get pods -A` | List pods in all namespaces |
| `kubectl describe pod <pod>` | Describe pod |
| `kubectl logs <pod>` | Show logs |
| `kubectl logs -f <pod>` | Follow logs |
| `kubectl exec -it <pod> -- bash` | Shell into pod |
| `kubectl delete pod <pod>` | Delete pod |

---

## 🟩 Deployments

| Command | Description |
|--------|-------------|
| `kubectl get deployments` | List deployments |
| `kubectl apply -f file.yaml` | Apply YAML |
| `kubectl delete -f file.yaml` | Delete from YAML |
| `kubectl rollout status deploy/<name>` | Watch rollout |
| `kubectl rollout restart deploy/<name>` | Restart deployment |
| `kubectl scale deploy/<name> --replicas=3` | Scale replicas |

---

## 🟩 Services & Networking

| Command | Description |
|--------|-------------|
| `kubectl get svc` | List services |
| `kubectl expose deploy/<name> --port=80` | Create service |
| `kubectl port-forward deploy/<name> 8080:80` | Port forward |

---

## 🟩 Namespaces

| Command | Description |
|--------|-------------|
| `kubectl get ns` | List namespaces |
| `kubectl create ns <name>` | Create namespace |
| `kubectl delete ns <name>` | Delete namespace |
| `kubectl config set-context --current --namespace=<ns>` | Set default namespace |

---

# 🌍 Terraform — Essential Commands

## 🟧 Initialize

| Command | Description |
|--------|-------------|
| `terraform init` | Initialize project |
| `terraform get` | Download modules |

---

## 🟧 Validate

| Command | Description |
|--------|-------------|
| `terraform fmt` | Format configuration |
| `terraform validate` | Validate syntax |
| `terraform graph` | View dependency graph |

---

## 🟧 Plan

| Command | Description |
|--------|-------------|
| `terraform plan` | Show execution plan |
| `terraform plan -out=tfplan` | Save plan |

---

## 🟧 Apply / Destroy

| Command | Description |
|--------|-------------|
| `terraform apply` | Apply changes |
| `terraform apply tfplan` | Apply saved plan |
| `terraform destroy` | Destroy infrastructure |

---

## 🟧 State Management

| Command | Description |
|--------|-------------|
| `terraform state list` | List managed resources |
| `terraform state show <resource>` | Show state |
| `terraform state rm <resource>` | Remove from state |
| `terraform refresh` | Refresh state |

---

## 🟧 Workspaces

| Command | Description |
|--------|-------------|
| `terraform workspace list` | List workspaces |
| `terraform workspace new dev` | Create workspace |
| `terraform workspace select dev` | Switch workspace |


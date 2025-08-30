# DevOps ToDo List - Kubernetes & Ingress Setup

## Prerequisites

- Docker installed
- Kubernetes cluster (Minikube, Docker Desktop, or cloud provider)
- kubectl CLI
- Python 3.8+
- Git

## 1. Clone the Repository

```sh
git clone <your-repo-url>
cd devops_todolist_kubernetes_task_10_ingress
```

## 2. Build & Run Locally (Optional)

```sh
cd src
pip install -r requirements.txt
python manage.py migrate
python manage.py runserver
```

## 3. Build Docker Image

```sh
docker build -t todolist-app:latest src/
```

## 4. Kubernetes Deployment

### 4.1. Create Namespace

```sh
kubectl apply -f .infrastructure/app/ns.yml
```

### 4.2. Deploy MySQL

```sh
kubectl apply -f .infrastructure/mysql/ns.yml
kubectl apply -f .infrastructure/mysql/configMap.yml
kubectl apply -f .infrastructure/mysql/secret.yml
kubectl apply -f .infrastructure/mysql/service.yml
kubectl apply -f .infrastructure/mysql/statefulSet.yml
```

### 4.3. Deploy Application

```sh
kubectl apply -f .infrastructure/app/configMap.yml
kubectl apply -f .infrastructure/app/secret.yml
kubectl apply -f .infrastructure/app/pv.yml
kubectl apply -f .infrastructure/app/pvc.yml
kubectl apply -f .infrastructure/app/deployment.yml
kubectl apply -f .infrastructure/app/clusterIp.yml
kubectl apply -f .infrastructure/app/hpa.yml
```

### 4.4. Set Up Ingress

```sh
kubectl apply -f .infrastructure/ingress/ingress.yml
```

> **Note:** Ensure your cluster has an ingress controller (e.g., NGINX).

## 5. Access the Application

- Find the ingress IP or domain:
  ```sh
  kubectl get ingress -n <namespace>
  ```
- Open in browser: `http://<ingress-ip-or-domain>/`

## 6. Useful Commands

- View pods:
  ```sh
  kubectl get pods -n <namespace>
  ```
- View services:
  ```sh
  kubectl get svc -n <namespace>
  ```
- View logs:
  ```sh
  kubectl logs <pod-name> -n <namespace>
  ```

## 7. Troubleshooting

- Check pod status:
  ```sh
  kubectl describe pod <pod-name> -n <namespace>
  ```
- Check events:
  ```sh
  kubectl get events -n <namespace>
  ```

---

For more details, check the manifests in `.infrastructure/` and source code
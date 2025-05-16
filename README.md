# Kubernetes Observability Project using Argo CD, Prometheus, and Grafana

This project demonstrates a complete DevOps pipeline where a static website is containerized using Docker, deployed to a Kubernetes cluster using GitOps with Argo CD, and monitored with Prometheus and Grafana using the `kube-prometheus-stack`.

---

## 📌 Project Summary

- **App**: Static HTML/CSS website
- **Containerization**: Docker
- **Registry**: DockerHub
- **Deployment**: Kubernetes (with Argo CD GitOps)
- **Monitoring Stack**: Prometheus + Grafana
- **Visualization**: Pod-level CPU/Memory usage, real-time metrics via PromQL

---

## 🚀 What This Project Covers

- Dockerizing and pushing a static website to DockerHub
- Writing Kubernetes manifests with CPU/Memory resource requests
- GitOps-based deployment using Argo CD
- Installing Prometheus and Grafana using Helm
- Live monitoring with Prometheus queries and Grafana dashboards

---

## 🛠️ Tools & Technologies Used

| Tool/Service      | Purpose                               |
|-------------------|----------------------------------------|
| Docker            | Containerize the static web app        |
| DockerHub         | Store and pull Docker images           |
| Kubernetes        | Container orchestration                |
| Argo CD           | GitOps-based application deployment    |
| Helm              | Install kube-prometheus-stack          |
| Prometheus        | Collect metrics from K8s resources     |
| Grafana           | Visualize metrics in real time         |
| PromQL            | Query live metrics from Prometheus     |

---

## 🚀 Create DockerFile

![dockerfile](https://github.com/user-attachments/assets/234bc0ca-a600-46c7-bb3c-7182ec6ff919)

```bash
docker build -t lovish56456/observability:01 .
docker push lovish56456/observability:01
```
---

## ☸️ Kubernetes Manifests

- Deployment.yml
- Service.yml

## 🚀 Deployment with Argo CD
``` bash
kubectl create namespace argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
kubectl --namespace argocd port-forward svc/argocd-server 8080:443
```
- Connect Argo CD to your GitHub repo.
- Sync the deployment using the UI or CLI.
- The app is deployed to observe namespace.
  
![argo](https://github.com/user-attachments/assets/c9ec1c95-1715-4629-b9fe-34797bd0b1b1)


---

## 📈 Prometheus & Grafana Setup
Install kube-prometheus-stack using Helm
``` bash
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
helm install monitoring prometheus-community/kube-prometheus-stack
```
Access Grafana
``` bash
kubectl port-forward svc/monitoring-grafana 3000:80
```

---

## 📊 Prometheus Metrics
``` bash
# Live CPU usage
rate(container_cpu_usage_seconds_total{namespace="observe"}[5m])

# Live Memory usage
container_memory_usage_bytes{namespace="observe"}

# Requested CPU from YAML
kube_pod_container_resource_requests_cpu_cores{namespace="observe"}
```
## Prometheus
![prome1](https://github.com/user-attachments/assets/89f9d029-b2aa-4215-8f42-c0a4fb338140)

![prome2](https://github.com/user-attachments/assets/ac684883-4737-48df-bb93-e98132ce573b)

![prome3](https://github.com/user-attachments/assets/6b11110d-085c-46ba-9c73-bb65adaa41bc)

## Grafana
![grafana2](https://github.com/user-attachments/assets/f246a14c-40fa-4749-9b21-a74fd11212d8)

## License

[MIT](https://choosealicense.com/licenses/mit/)



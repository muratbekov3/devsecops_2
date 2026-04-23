# 🚀 DevOps GitOps Project (ArgoCD + Kubernetes + Observability)

## 📌 Overview

This project demonstrates a complete DevSecOps pipeline using GitOps principles.
The application is automatically built, containerized, deployed to Kubernetes, and monitored using a full observability stack.

The goal of this project is to simulate a real-world DevOps environment with CI/CD, GitOps, and monitoring.

---

## 🧠 Architecture

```text
Developer → GitHub → CI (GitHub Actions) → Docker Hub
                                      ↓
                                  ArgoCD
                                      ↓
                                 Kubernetes (Minikube)
                                      ↓
        ┌───────────────┬───────────────┬───────────────┐
        ↓               ↓               ↓
   Prometheus        Loki         Alertmanager
   (Metrics)         (Logs)        (Alerts)
        ↓               ↓
            Grafana (Dashboards)
```

---

## 🛠️ Tech Stack

* Kubernetes (Minikube)
* ArgoCD (GitOps deployment)
* GitHub Actions (CI/CD)
* Docker (containerization)
* Prometheus (metrics collection)
* Grafana (visualization)
* Loki (log aggregation)
* Alertmanager (alerting)

---

## ⚙️ Project Structure

```text
devsecops-project/
├── app-source/                # Application code + Dockerfile
├── gitops-repo/
│   └── apps/
│           ├── deployment.yaml
│           └── service.yaml
├── .github/workflows/         # CI pipeline (GitHub Actions)
└── README.md
```

---

## 🔄 CI/CD Pipeline (GitHub Actions)

1. Code is pushed to GitHub
2. Pipeline automatically:

   * Builds Docker image
   * Tags image using commit SHA
   * Pushes image to Docker Hub
3. ArgoCD detects changes and deploys to Kubernetes

### 🔑 Key Concept

Images are tagged using commit SHA to ensure traceability and easy rollback.

---

## ☸️ GitOps Deployment (ArgoCD)

* Kubernetes manifests are stored in a separate GitOps repository
* ArgoCD continuously watches the repository
* Any change is automatically synchronized to the cluster

### Benefits:

* Declarative deployments
* No manual kubectl apply
* Self-healing infrastructure

---

## 📊 Monitoring & Observability

The monitoring stack was deployed locally on Kubernetes (Minikube) using Helm.

### 🔹 Metrics — Prometheus

* Installed via kube-prometheus-stack
* Collects:

  * CPU usage
  * Memory usage
  * Pod metrics

### 🔹 Visualization — Grafana

* Connected to Prometheus and Loki
* Custom dashboards created for:

  * CPU usage
  * Memory usage
  * Pod status

### 🔹 Logging — Loki

* Aggregates logs from Kubernetes pods
* Integrated with Grafana for log exploration

### 🔹 Alerting — Alertmanager

* Processes alerts generated from Prometheus rules
* Example alert:

  * High CPU usage detection

### 🧠 Deployment Approach

* Monitoring stack deployed using Helm (manual)
* Runs inside the Kubernetes cluster

---

## 🚀 How to Run the Project

### 1. Start Kubernetes cluster

```bash
minikube start
```

---

### 2. Install ArgoCD

```bash
kubectl create namespace argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
```

---

### 3. Apply ArgoCD Application

```bash
kubectl apply -f app.yaml
```

---

### 4. Access the application

```bash
minikube service devsecops-app
```

---

### 5. Access Grafana

```bash
kubectl port-forward svc/monitoring-grafana 3000:80
```

Open:

```
http://localhost:3000
```

---

## 📈 Features

* GitOps-based deployment using ArgoCD
* Automated CI/CD pipeline
* Docker image versioning using commit SHA
* Kubernetes-based application deployment
* Full observability stack (metrics, logs, alerts)
* Custom Grafana dashboards

---

## 🧠 Key Learnings

* Understanding GitOps workflow using ArgoCD
* Building CI/CD pipelines with GitHub Actions
* Debugging Kubernetes services and networking
* Integrating monitoring and logging systems
* Managing containerized applications in Kubernetes

---

## ⚠️ Challenges Faced

* ArgoCD syncing empty or incorrect paths
* Docker authentication issues in CI pipeline
* Loki and Grafana connectivity troubleshooting
* Kubernetes service exposure (NodePort)

---

## 👨‍💻 Author

Akylbek Muratbek uulu

---
<img src="./Screenshot from 2026-04-23 17-02-18.png" alt="argocd" width="900">
<img src="./Screenshot from 2026-04-23 17-06-23.png" alt="argocd" width="900">
<img src="./Screenshot from 2026-04-23 17-07-03.png" alt="argocd" width="900">


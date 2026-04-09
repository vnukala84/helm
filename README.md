# 🚀 Product Service - Helm + GitOps Deployment

This repository contains a **production-ready Helm chart** for deploying the Product Service into Kubernetes, integrated with a GitOps workflow using ArgoCD.

---

## 📌 Overview

- 📦 Package Kubernetes manifests using Helm
- 🔄 Enable automated deployments via GitOps
- 🚀 Deploy consistently across environments

---

## 🏗️ Architecture

Developer → GitHub Repo → ArgoCD → Kubernetes Cluster

- Code pushed to GitHub triggers ArgoCD sync
- ArgoCD deploys Helm chart to Kubernetes

---

## 📁 Project Structure

helm/
└── product-service/
    ├── Chart.yaml
    ├── values.yaml
    └── templates/
        ├── deployment.yaml
        ├── service.yaml

---

## ⚙️ Prerequisites

- Kubernetes Cluster (Minikube / EKS / AKS / GKE)
- Helm 3+
- kubectl configured
- ArgoCD installed

---

## 🚀 Helm Deployment

### Install

```bash
helm install product-release ./product-service
```

### Upgrade

```bash
helm upgrade product-release ./product-service
```

### Uninstall

```bash
helm uninstall product-release
```

---

## 🔍 Verify Deployment

```bash
kubectl get pods
kubectl get svc
```

---

## 🌍 Access Application

```bash
kubectl port-forward svc/product-service 8080:80
```

Open: http://localhost:8080

---

## 🔄 GitOps with ArgoCD

### Step 1: Create Application

```bash
argocd app create product-service   --repo https://github.com/vnukala84/helm.git   --path product-service   --dest-server https://kubernetes.default.svc   --dest-namespace default
```

### Step 2: Sync Application

```bash
argocd app sync product-service
```

### Step 3: Check Status

```bash
argocd app get product-service
```

---

## 📊 Key Features

- ✅ Parameterized deployments using Helm
- ✅ Environment-specific configurations via values.yaml
- ✅ GitOps-based continuous delivery
- ✅ Easy rollback using Helm revisions

---

## 🛠️ Customization

Update values.yaml:

```yaml
replicaCount: 2

image:
  repository: venkat8430/product-service
  tag: latest

service:
  type: ClusterIP
  port: 80
```

---

## 🔁 CI/CD Flow

1. Developer updates code or Helm chart
2. Push to GitHub
3. ArgoCD detects changes
4. Syncs automatically to Kubernetes

---

## 📌 Future Enhancements

- 🔐 Add Helm Secrets for secure values
- 📊 Integrate Prometheus + Grafana
- 🚀 Multi-environment (dev/stage/prod) setup
- 🔄 Auto-sync enabled in ArgoCD

---

## 👨‍💻 Author

**Venkat Nukala**

- DevOps Engineer | Cloud | Kubernetes | GitOps

---

## ⭐ Support

If you like this project, give it a ⭐ on GitHub!


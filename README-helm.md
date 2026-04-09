📦 Product Service – Helm Chart
🚀 Overview

This repository contains a Helm chart for deploying the product-service application on Kubernetes.

It demonstrates:

Helm templating
Configurable deployments using values.yaml
Kubernetes resource management (Deployment, Service)
Production-ready structure for DevOps workflows
📂 Project Structure
product-service/
├── Chart.yaml          # Helm chart metadata
├── values.yaml         # Configurable values
├── templates/
│   ├── deployment.yaml # Kubernetes Deployment
│   ├── service.yaml    # Kubernetes Service
│   └── _helpers.tpl    # Helper templates
⚙️ Prerequisites

Make sure you have:

Kubernetes cluster (Minikube / EKS / AKS / OpenShift)
Helm installed
kubectl configured

Check versions:

helm version
kubectl version --client
🛠️ Configuration

Edit values.yaml to customize deployment:

replicaCount: 2

image:
  repository: venkat8430/product-service
  tag: v1
  pullPolicy: IfNotPresent

service:
  type: ClusterIP
  port: 80
🚀 Deployment
1. Install Helm Chart
helm install product-release .
2. Verify Deployment
helm list
kubectl get pods
kubectl get svc
3. Access Application

If using NodePort:

kubectl get svc

If using port-forward:

kubectl port-forward svc/product-service 8080:80

Access:

http://localhost:8080
🔄 Upgrade Application

Update values.yaml (e.g., image tag):

tag: v2

Then run:

helm upgrade product-release .
⏪ Rollback

View history:

helm history product-release

Rollback:

helm rollback product-release 1
🧹 Uninstall
helm uninstall product-release
⚠️ Common Issues
❌ Service Already Exists Error
Service "product-service" exists and cannot be imported into Helm
✅ Solution

Delete existing resource:

kubectl delete svc product-service

OR add Helm ownership manually:

kubectl label svc product-service app.kubernetes.io/managed-by=Helm
kubectl annotate svc product-service meta.helm.sh/release-name=product-release
kubectl annotate svc product-service meta.helm.sh/release-namespace=default
🧠 Key Concepts
Chart → Helm package
Release → Running instance of a chart
Values.yaml → Configuration file
Templates → Dynamic Kubernetes YAML
🔁 GitOps Integration (Optional)

This Helm chart can be used with GitOps tools like Argo CD.

Steps:

Push this repo to Git
Connect repo in Argo CD
Deploy using Helm chart path
Sync changes automatically
📌 Best Practices

Use dynamic naming:

name: {{ .Release.Name }}-product-service
Keep values configurable
Avoid hardcoding image tags
Use labels consistently

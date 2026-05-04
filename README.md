# ⚙️ GitOps Repository - Register App Deployment

This repository contains Kubernetes manifests and GitOps configuration for deploying the Register application on AWS EKS using ArgoCD.

---

## 📌 Overview

Implements a GitOps workflow where ArgoCD continuously monitors this repository and syncs changes automatically to the Kubernetes cluster.

---

## 🧱 Tech Stack

- Kubernetes (EKS)
- ArgoCD
- Prometheus
- Grafana
- Loki
- Promtail
- Alertmanager

---

## 🔁 GitOps Workflow

1. CI pipeline updates image tag in manifests
2. Changes pushed to this repository
3. ArgoCD detects changes
4. Automatic deployment to EKS cluster

---

## 📂 Repository Structure

- `deployment.yaml` → Application deployment
- `service.yaml` → Kubernetes service
- `alerts.yaml` → Prometheus alert rules
- `alertmanager-config.yaml` → Alert configuration (SMTP)
- `loki.yaml` → Loki setup
- `promtail.yaml` → Log collection

---

## 📊 Observability

- Prometheus → Metrics collection
- Grafana → Dashboards
- Loki + Promtail → Logging
- Alertmanager → Email alerts

---

## 🚨 Features

✔ GitOps-based deployment  
✔ Automated sync via ArgoCD  
✔ Monitoring & logging stack  
✔ Alerting via Email  

---

## 🔗 Application Repo

👉 https://github.com/YOUR_USERNAME/end-to-end-ci-cd-pipeline

---

## 💡 Note

This repository represents the CD (GitOps) layer of a full DevOps pipeline.


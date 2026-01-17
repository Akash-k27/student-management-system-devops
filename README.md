# Student Management System — DevOps & Kubernetes Project (EKS + GitOps)

This repository demonstrates a complete **cloud-native DevOps implementation** of a Django-based Student Management System using modern industry tools including **AWS EKS, Docker, Terraform, GitHub Actions, ArgoCD (GitOps), and Prometheus/Grafana monitoring**.

This project transforms a simple Django application into a fully automated, scalable, observable, and production-like system running on Kubernetes.

---

## 🎯 Project Objectives

The key goals of this project were to:

- Containerize a Django application using **Docker**
- Build a **CI pipeline with GitHub Actions**
- Deploy infrastructure as code using **Terraform**
- Run the application on **AWS EKS (Kubernetes)**
- Implement **GitOps using ArgoCD**
- Add **cluster and application monitoring with Prometheus & Grafana**
- Automate image updates using **ArgoCD Image Updater**

---
## 🏗️ High-Level Architecture

Developer → GitHub → GitHub Actions (CI)
↓
Build Docker Image
↓
Push to AWS ECR
↓
Terraform provisions:
  - VPC
  - Subnets
  - IAM roles
  - EKS Cluster + Node Groups
    ↓
    ArgoCD watches Git repo (GitOps)
    ↓
    Kubernetes deploys:
  - Django app pods
  - AWS Load Balancer
  - Prometheus + Grafana
    ↓
    Users access app via AWS ELB

---

## 🛠️ Tech Stack

|------------------------|----------------------|
| Layer                  | Tool                 |
|------------------------|----------------------|
| Application            | Django 4             |
| Containerization       | Docker               |
| CI/CD                  | GitHub Actions       |
| Infrastructure as Code | Terraform            |
| Cloud Provider         | AWS                  |
| Kubernetes Platform    | Amazon EKS           |
| GitOps                 | ArgoCD               |
| Monitoring             | Prometheus + Grafana |
| Registry               | AWS ECR              |
| Database               | SQLite (for demo)    |
|------------------------|----------------------|


---

## 🚀 What Was Implemented

### 1️⃣ Dockerized Django App

- Created a `Dockerfile`
- Used a lightweight Python base image
- Added migrations via an init container in Kubernetes
- Configured `ALLOWED_HOSTS` using environment variables

---

### 2️⃣ CI Pipeline with GitHub Actions

The GitHub Actions workflow:

- Builds the Docker image on every push to `main`
- Tags image with Git commit SHA
- Pushes image to **AWS ECR**

---

### 3️⃣ AWS Infrastructure with Terraform

Terraform provisions:

- Custom VPC  
- Public & private subnets  
- Internet Gateway  
- Route tables  
- EKS cluster  
- Managed node groups  

---

### 4️⃣ Kubernetes Deployment (EKS)

Kubernetes resources include:

- `Deployment` with 2 replicas  
- `Service` of type `LoadBalancer`  
- Init container for database migrations  
- Image pull secret for ECR  

---

### 5️⃣ GitOps with ArgoCD

Instead of running `kubectl apply` manually:

- All Kubernetes manifests are stored in Git under:

argocd/k8s/

- ArgoCD automatically syncs changes from Git to EKS
- Ensures cluster always matches repository state

---

### 6️⃣ Automated Image Updates

ArgoCD Image Updater:

- Watches AWS ECR for new images
- Automatically updates Kubernetes Deployment with latest image tag
- Triggers rolling updates without manual intervention

---

### 7️⃣ Monitoring with Prometheus & Grafana

Installed using Helm:

- Prometheus collects cluster and pod metrics  
- Grafana visualizes dashboards  
- Enabled monitoring for:
  - Node CPU & Memory  
  - Pod health  
  - Kubernetes workloads  

---

## 📁 Repository Structure

student-management-system/
│
├── app/ # Django application
├── Dockerfile # Container build file
├── docker-compose.yml # Local testing
├── .github/workflows/ # CI pipeline
├── terraform/ # Infrastructure as Code
├── argocd/
│ └── k8s/ # Kubernetes manifests (GitOps)
│ ├── deployment.yaml
│ └── service.yaml
└── README.md # This documentation


---

## 💡 What I Learned

Through this project I gained hands-on experience with:

- Docker & container best practices  
- Kubernetes concepts: Pods, Deployments, Services  
- AWS EKS networking and security  
- Terraform modular design  
- GitOps workflow with ArgoCD  
- Observability with Prometheus & Grafana  
- CI/CD automation and artifact management in ECR  

---

## 📌 Future Improvements (Optional)

- Replace SQLite with PostgreSQL on RDS  
- Add HTTPS using AWS ACM + ALB  
- Implement Prometheus alerts  
- Add HPA (Horizontal Pod Autoscaler)  
- Integrate Slack alerts for failures  

---

## 👤 Author

**Akash K**  
DevOps & Cloud   
AWS | Kubernetes | Terraform | GitHub Actions | ArgoCD



# Project : Application Deployment on Kubernetes Cluster utilizing EKS, AWS

## CRUD Operations
- Create
- Read
- Update
- Delete

## Project Overview
This project focuses on deployment of a web application to a Kubernetes cluster using AWS EKS.

### Key Benefits of Kubernetes
- Auto Healing
- Auto Scaling
- Load Balancing
- Security
- Resilience

## Services Used
- AWS EC2
- AWS RDS (MySQL)
- Docker
- Docker Hub
- AWS EKS (Kubernetes)

## Project Workflow

### 1. Application Preparation
- Create EC2 instance and clone the repository
- Create MySQL database (RDS)
- Update `app.js` with correct database connection details
- Build Docker image  
  ```bash
  docker build -t ddinuka/crud .
  ```
- Test locally  
  ```bash
  docker run -p 3000:3000 ddinuka/crud
  ```

### 2. Push Image to Docker Hub
- Create repository `crud` in Docker Hub
- Tag and push image  
  ```bash
  docker push ddinuka/crud:latest
  ```

### 3. Create EKS Cluster
- Create EKS Cluster (Control Plane)
- Configure VPC, subnets, and cluster access
- Enable required add-ons (CoreDNS, kube-proxy, AWS VPC CNI)
- Create Node Group
  - Instance type: t3.medium
  - OS: Amazon Linux
  - Desired nodes: 2

## Kubernetes Architecture Overview

### Control Plane (Managed by AWS)
- kube-apiserver
- etcd
- kube-scheduler
- kube-controller-manager
- cloud-controller-manager

### Worker Nodes
- kubelet
- kube-proxy
- Container Runtime (via CRI)

### CRI (Container Runtime Interface)
The interface that allows Kubernetes to use container runtimes (e.g., containerd) to run pods.

## Final Outcome
Successfully deployed a Node.js + MySQL CRUD application on AWS EKS with:
- Dockerized application
- Image hosted on Docker Hub
- Fully functional Kubernetes cluster on AWS EKS
- Auto-scaling, self-healing, and resilient deployment

**Project Status: Completed and Deployed**

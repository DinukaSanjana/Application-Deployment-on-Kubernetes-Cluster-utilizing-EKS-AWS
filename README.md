# Project: Application Deployment on Kubernetes Cluster utilizing EKS, AWS

## CRUD Application  
- Create  
- Read  
- Update  
- Delete  

This project focuses on deployment of a web application to a Kubernetes cluster.  
The major benefits of deploying a web-app on Kubernetes cluster:  
- Auto Healing  
- Auto Scaling  
- Load Balancing  
- Security  
- Resilience  

## Services Used  
- AWS EC2  
- AWS RDS / DigitalOcean Managed MySQL  
- Docker  
- Docker Hub  
- AWS EKS (Kubernetes)  

## Step-by-Step Project Execution

### 1. Create EC2 Instance and Clone Repository  
Launch an EC2 instance and clone the CRUD application repository from GitHub.

### 2. Create Database and Update Connection in app.js  
Create a MySQL database (DigitalOcean or AWS RDS).  
Update `app.js` with correct database credentials: host, user, password, database name, port, and SSL settings.

### 3. Build Docker Image  
```bash
docker build -t ddinuka/crud .
```
Builds the Docker image from the Dockerfile in the repository.

### 4. Test Application Locally  
```bash
docker run -p 3000:3000 ddinuka/crud
```
Runs the container locally to verify the app connects to the database and works.

### 5. Fix Database Connectivity Issues  
- Add your EC2 public IP to DigitalOcean Database → Trusted Sources  
  Allows outbound traffic from your server to reach the managed database.  
- Change `package.json`: `"mysql"` → `"mysql2"`  
  Required because newer MySQL versions use caching_sha2_password authentication (not supported by old mysql package).  
- Change `app.js`: `require('mysql')` → `require('mysql2')`  
  Uses the updated driver that supports modern MySQL authentication.

### 6. Rebuild and Push to Docker Hub  
Create a repository named `crud` in Docker Hub.  
```bash
docker push ddinuka/crud:latest
```
Makes the image publicly accessible for Kubernetes to pull.

### 7. Create EKS Cluster  
- Control Plane (Brain of the cluster – Fully managed by AWS)  
- Create Node Group with 3 nodes (t3.medium, Amazon Linux 2)

### 8. Configure Local Machine / EC2 to Manage EKS  
```bash
aws configure
```
Configures AWS CLI with Access Key, Secret Key, and region.

```bash
aws eks update-kubeconfig --name <cluster-name> --region <region>
```
Updates kubeconfig file so `kubectl` commands talk to your EKS cluster.

### 9. Verify Cluster Access  
```bash
kubectl get nodes
```
Lists all 3 worker nodes – confirms successful connection and node registration.

### 10. Deploy Application  
```bash
kubectl apply -f app.yaml
```
Deploys the CRUD application (Deployment + Replicas) to the cluster.

### 11. Expose Application with LoadBalancer Service  
```bash
kubectl apply -f svc.yaml
```
Creates a LoadBalancer service (AWS ELB) to expose the app publicly.

### 12. Verify Deployment  
```bash
kubectl get deploy
```
Shows running deployments.

```bash
kubectl get pods
```
Shows pod status and names.

### 13. Test Self-Healing (Auto Healing)  
```bash
kubectl delete pod <pod-name>
```
Manually deletes a running pod.

```bash
kubectl get pods
```
New pod automatically starts within seconds – proves Kubernetes self-healing.

### 14. Service Types in Kubernetes  
- ClusterIP → Internal only  
- NodePort → Exposes on node IP + high port  
- LoadBalancer → Creates public AWS Elastic Load Balancer (used in this project)

### 15. Get Public Access URL  
```bash
kubectl get service
```
Look for the EXTERNAL-IP of the LoadBalancer service.  
Users access the CRUD app via this public DNS/IP.  
Users cannot SSH directly into nodes – access only through LoadBalancer → Pods.

## Final Result  
Successfully deployed a full-stack Node.js + MySQL CRUD application on AWS EKS with:  
- Dockerized application  
- Public image in Docker Hub  
- 3-node Kubernetes cluster  
- LoadBalancer exposure  
- Demonstrated self-healing  
- Production-like secure and resilient architecture  

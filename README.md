# ☸️ WordPress on Amazon EFS using Kubernetes (EKS)

## 📌 Overview
This project demonstrates how to **deploy WordPress with MySQL on Kubernetes using Amazon EFS (Elastic File System) as persistent storage**.

It covers:
- Kubernetes cluster setup (EKS)
- Dynamic persistent storage using **EFS**
- WordPress & MySQL deployments
- StorageClasses, PersistentVolumes, and PVCs
- Secure RBAC configuration

This setup enables **high availability, shared storage, and data persistence**, which is critical for **production WordPress workloads**.

---

## 🧠 Problem Statement
Running WordPress on Kubernetes requires:
- Persistent shared storage
- High availability across pods
- Safe handling of application data

Default Kubernetes storage (like hostPath) is:
- Not scalable
- Not suitable for production
- Node-dependent

This project solves the problem by using **Amazon EFS**, which provides:
- Shared filesystem
- Elastic scaling
- Multi-AZ availability

---

## 🏗️ Architecture & Workflow
User
↓
LoadBalancer / Service
↓
WordPress Pods (Kubernetes)
↓
PersistentVolumeClaim (PVC)
↓
StorageClass
↓
Amazon EFS
↓
MySQL Database Pod

yaml
Copy code

---

## 🛠️ Tech Stack
- **Container Orchestration:** Kubernetes (EKS)
- **Cloud Provider:** AWS
- **Storage:** Amazon EFS
- **Application:** WordPress
- **Database:** MySQL
- **Automation:** YAML manifests
- **Security:** RBAC

---

## ⚙️ Key Features
- WordPress deployment on Kubernetes
- Persistent shared storage using Amazon EFS
- Dynamic provisioning using EFS provisioner
- Kubernetes RBAC for secure access
- StorageClass and PVC-based storage management
- Production-style Kubernetes storage setup

---

## 📂 Project Structure

```text
Wordpress-on-EFS/
├── create-efs-provisioner.yaml   # EFS dynamic provisioner
├── create-rbac.yaml              # RBAC permissions
├── create-storage.yaml           # StorageClass & PV config
├── deploy-mysql.yaml             # MySQL deployment
├── deploy-wordpress.yaml         # WordPress deployment
├── enable-efs.md                 # EFS setup instructions
│
├── ekscluster/
│   ├── cluster.yml               # EKS cluster creation
│   ├── fcluster.yml              # Cluster configuration
│   ├── pvc.yml                   # PersistentVolumeClaim
│   ├── sc.yml                    # StorageClass
│   └── README.md
└── README.md

🚀 How to Run the Project

1️⃣ Prerequisites
AWS account

EKS cluster running

kubectl configured

AWS CLI configured

EFS filesystem created

Worker nodes with EFS mount support

2️⃣ Configure EFS
Follow instructions in:

text
Copy code
enable-efs.md
Ensure:

EFS is in the same VPC as EKS

Security groups allow NFS (2049)

3️⃣ Apply RBAC & EFS Provisioner
bash
Copy code
kubectl apply -f create-rbac.yaml
kubectl apply -f create-efs-provisioner.yaml

4️⃣ Create StorageClass
bash
Copy code
kubectl apply -f create-storage.yaml

5️⃣ Deploy MySQL
bash
Copy code
kubectl apply -f deploy-mysql.yaml

6️⃣ Deploy WordPress
bash
Copy code
kubectl apply -f deploy-wordpress.yaml

7️⃣ Verify Deployment
bash
Copy code
kubectl get pods
kubectl get pvc
kubectl get svc
Access WordPress using the exposed service endpoint.

📊 Outcome / Results

WordPress running on Kubernetes

Data persisted using Amazon EFS

Pods can restart without data loss

Shared storage across replicas

Production-ready Kubernetes storage setup

🧪 What I Learned

Kubernetes persistent storage concepts

Using Amazon EFS with Kubernetes

Dynamic provisioning using storage classes

RBAC security in Kubernetes

Running stateful workloads in Kubernetes

🔮 Future Enhancements

Add Ingress controller with TLS

Use RDS instead of pod-based MySQL

Enable WordPress auto-scaling

Add monitoring using Prometheus & Grafana

Implement backups for EFS data

Convert manifests into Helm charts


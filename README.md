# 🚀 Amazon Elastic Kubernetes Service (EKS) – Complete Guide

This repository contains a detailed step-by-step guide to setting up, configuring, and managing **Amazon Elastic Kubernetes Service (EKS)**. Ideal for beginners to intermediate learners looking to understand Kubernetes on AWS.

---

## 📌 What is Amazon EKS?

**Amazon Elastic Kubernetes Service (EKS)** is a managed Kubernetes service provided by AWS. It helps you run Kubernetes without having to manage your own control plane or nodes manually.

---

## ✅ Key Benefits of EKS

- 🔄 **Scalability** – Easily scale your applications as demand grows.
- 🔒 **Security & Compliance** – Integrated with IAM and fine-grained access controls.
- 💡 **High Availability** – Runs control plane instances across multiple AZs.
- 🔧 **Reduced Operational Overhead** – AWS manages control plane components.

---

## 🧰 Prerequisites

- An AWS account (Free Tier works for basic usage)
- Admin-level IAM access
- Ubuntu-based EC2 instance or local terminal with internet access

---

## 🛠️ Step-by-Step Setup Instructions

### 1. ✅ AWS CLI Installation

```bash
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
sudo apt install unzip
unzip awscliv2.zip
sudo ./aws/install
```

### 2. ⚙️ Configure AWS CLI

```bash
aws configure
# Provide Access Key, Secret Key, Region, Output Format
```

---

### 3. 🔐 IAM Role Setup for EKS

1. Go to IAM → Create User → `eks-admin`
2. Attach the policy `AdministratorAccess`
3. Generate Access Keys for programmatic access

---

### 4. 🧱 Install `kubectl`

```bash
curl -o kubectl https://amazon-eks.s3.us-west-2.amazonaws.com/1.19.6/2021-01-05/bin/linux/amd64/kubectl
chmod +x ./kubectl
sudo mv ./kubectl /usr/local/bin
kubectl version --short --client
```

---

### 5. 📦 Install `eksctl`

```bash
curl --silent --location "https://github.com/weaveworks/eksctl/releases/latest/download/eksctl_$(uname -s)_amd64.tar.gz" | tar xz -C /tmp
sudo mv /tmp/eksctl /usr/local/bin
eksctl version
```

---

## ☸️ Create an EKS Cluster

```bash
eksctl create cluster \
--name <cluster-name> \
--region <region> \
--nodegroup-name standard-workers \
--node-type t3.medium \
--nodes 2 \
--nodes-min 1 \
--nodes-max 3 \
--managed
```

---

## 🔌 Connect to the EKS Cluster

```bash
aws eks update-kubeconfig --region <region> --name <cluster-name>
kubectl get nodes
```

---

## 📦 Basic to Advanced `kubectl` Commands

### 🔍 Get Cluster Info

```bash
aws eks describe-cluster --name <cluster-name> --region <region>
```

### 🚀 Deploy an App

```bash
kubectl apply -f <your-app.yaml>
```

### 📈 Scale a Deployment

```bash
kubectl scale deployment <deployment-name> --replicas=3
```

### 🛡️ View Namespaces & Pods

```bash
kubectl get namespaces
kubectl get pods -n <namespace>
```

### 🔄 Rolling Updates

```bash
kubectl set image deployment/<deployment-name> <container-name>=<new-image>
```

### 💾 Persistent Volume Example

```bash
kubectl apply -f pv-definition.yaml
```

### ⚙️ Enable HPA (Horizontal Pod Autoscaling)

```bash
kubectl autoscale deployment <deployment-name> --min=3 --max=10 --cpu-percent=70
```

---

## 🧠 Advanced Concepts to Explore

- **Fargate with EKS** – Serverless compute engine for containers
- **EKS Add-ons** – Logging, monitoring, CoreDNS, kube-proxy, VPC CNI
- **IAM Roles for Service Accounts (IRSA)**
- **Ingress Controller Setup with ALB/Nginx**
- **Service Mesh (AWS App Mesh + Istio)**
- **CI/CD Integration with CodePipeline or GitHub Actions**
- **Multi-Cluster Management with `kubefed`**
- **Cost Optimization using Cluster Autoscaler & Spot Instances**

---

## 📚 Useful Resources

- [EKS Documentation](https://docs.aws.amazon.com/eks/)
- [Kubernetes Official Site](https://kubernetes.io/)
- [eksctl GitHub](https://github.com/weaveworks/eksctl)
- [kubectl Cheat Sheet](https://kubernetes.io/docs/reference/kubectl/cheatsheet/)

---

## ✍️ Author

**Nilesh Ipane**  
AWS | DevOps Engineer  
📍 Pune, Maharashtra  
🔗 [https://www.linkedin.com/in/nilesh-lipane/)

---

## 🤝 Contributions

Feel free to fork, improve, or share your own EKS setup tricks. PRs are welcome!

---


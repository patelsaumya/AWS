# ☸️ Amazon EKS Overview

## 📋 Overview

**Amazon EKS (Elastic Kubernetes Service)** is a fully managed service that allows you to launch and manage Kubernetes clusters on AWS. EKS simplifies the complexity of running Kubernetes by managing the control plane for you.

---

## 🔍 What is Kubernetes?

**Kubernetes** is an open-source system used for managing, deploying, and scaling containerized applications. It typically manages Docker containers but can work with other container types as well.

### 🔑 Key Characteristics

- **Container orchestration** – Manages containerized applications
- **Deployment** – Deploys containers across nodes
- **Scaling** – Scales containers automatically
- **Cloud-agnostic** – Runs on AWS, Azure, GCP, on-premises
- **Open source** – Open-source technology

---

## 🏗️ Amazon EKS

### 📊 What is EKS?

**Amazon EKS** is a managed Kubernetes service that:
- **Launches Kubernetes clusters** – Create and manage Kubernetes on AWS
- **Managed service** – AWS manages the Kubernetes control plane
- **Simplifies Kubernetes** – Makes running Kubernetes easier
- **EC2 or Fargate** – Run pods on EC2 instances or Fargate (serverless)

### 🔄 How EKS Works

**EKS Architecture:**
```
EKS Cluster
├── EKS Nodes (EC2 Instances)
│   ├── Pod (Container)
│   └── Pod (Container)
└── EKS Nodes (EC2 Instances)
    └── Pod (Container)
```

**Process:**
1. **Create EKS cluster** – Launch Kubernetes cluster on AWS
2. **Launch containers** – Deploy Docker containers on cluster
3. **Pods created** – Kubernetes automatically creates pods
4. **Pods on nodes** – Pods launched onto EC2 instances (or Fargate)

---

## 🎯 Why Use EKS?

### ⚡ Managed Kubernetes

**Benefits:**
- **Simplifies Kubernetes** – Launching Kubernetes is hard, EKS makes it easier
- **Managed service** – AWS manages Kubernetes control plane
- **Less complexity** – Focus on applications, not infrastructure

### 🌐 Cloud-Agnostic

**Kubernetes Benefits:**
- **Multi-cloud** – Works on AWS, Azure, GCP
- **On-premises** – Can run on-premises infrastructure
- **Portable** – Learn once, deploy anywhere
- **Cloud-agnostic** – Not locked to one cloud provider

---

## 🏗️ Infrastructure Options

### 📊 EC2 or Fargate

**EKS Supports:**
- **EC2 instances** – Run pods on EC2 instances (EKS nodes)
- **Fargate** – Run pods on Fargate (serverless, no EC2)

**Choice:**
- **EC2** – More control, manage EC2 instances
- **Fargate** – Serverless, no EC2 management

---

## 📊 Summary

| Feature | Description |
|---------|-------------|
| **Service Type** | Managed Kubernetes service |
| **Purpose** | Launch and manage Kubernetes clusters |
| **Technology** | Kubernetes (open-source) |
| **Infrastructure** | EC2 instances or Fargate |
| **Key Benefit** | Simplifies Kubernetes management |
| **Cloud-Agnostic** | Works on multiple clouds |

---

## 🎯 Key Takeaways

- **EKS is managed Kubernetes** – Launch and manage Kubernetes clusters on AWS
- **Kubernetes is open-source** – System for managing containerized applications
- **Simplifies Kubernetes** – Makes running Kubernetes easier
- **EC2 or Fargate** – Run pods on EC2 instances or Fargate
- **Pods on nodes** – Containers run as pods on EKS nodes
- **Cloud-agnostic** – Kubernetes works on AWS, Azure, GCP, on-premises
- **Multi-cloud** – Use Kubernetes across multiple cloud providers

# 🐳 Amazon ECS Overview

## 📋 Overview

**Amazon ECS (Elastic Container Service)** is a fully managed container orchestration service that allows you to run Docker containers on AWS. You must provision and maintain EC2 instances, and ECS manages starting and stopping containers on those instances.

---

## 🔍 What is ECS?

**Amazon ECS** is a service that launches Docker containers on AWS. It manages container placement and lifecycle, but requires you to provision and maintain the underlying EC2 infrastructure.

### 🔑 Key Characteristics

- **Docker containers** – Runs Docker containers on AWS
- **EC2-based** – Must provision and maintain EC2 instances
- **Container orchestration** – AWS manages starting/stopping containers
- **Intelligent placement** – ECS places containers on EC2 instances automatically
- **Load balancer integration** – Integrates with Application Load Balancer

---

## 🏗️ How ECS Works

### 📊 Architecture

```
EC2 Instances (Provisioned by You)
├── EC2 Instance 1
│   ├── Container (App 1)
│   └── Container (App 2)
├── EC2 Instance 2
│   ├── Container (App 3)
│   └── Container (App 4)
└── EC2 Instance 3
    └── Container (App 5)
```

**Process:**
1. **Provision EC2 instances** – Create EC2 instances in advance
2. **ECS manages containers** – AWS starts/stops containers for you
3. **Intelligent placement** – ECS finds best EC2 instance for each container
4. **Load balancer** – Integrate with ALB for web applications

---

## ⚡ Key Features

- **Container management** – AWS handles container lifecycle
- **EC2 provisioning** – You must create and maintain EC2 instances
- **Intelligent scheduling** – ECS places containers optimally
- **ALB integration** – Works with Application Load Balancer

---

## 📊 Summary

| Feature | Description |
|---------|-------------|
| **Service Type** | Container orchestration service |
| **Infrastructure** | Must provision EC2 instances |
| **Container Management** | AWS manages container lifecycle |
| **Use Case** | Run Docker containers on AWS |

---

## 🎯 Key Takeaways

- **ECS runs Docker containers** – Launch containers on AWS
- **Must provision EC2** – Create and maintain EC2 instances yourself
- **AWS manages containers** – Starts/stops containers automatically
- **Intelligent placement** – ECS finds best EC2 instance for containers
- **ALB integration** – Works with Application Load Balancer

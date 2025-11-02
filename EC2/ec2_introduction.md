# Amazon EC2 - Introduction

## Overview

**Amazon EC2 (Elastic Compute Cloud)** is one of the most popular AWS services. It provides **Infrastructure as a Service (IaaS)**, allowing you to rent virtual servers (called **instances**) on demand.

With EC2, you can launch, configure, and manage virtual machines in the cloud, giving you complete control over your compute resources. Knowing how to use EC2 is fundamental to understanding how the cloud works.

---

## Key Components of EC2

EC2 is not just a single service—it includes several components that work together to deliver compute power at scale:

- **EC2 Instances** – Virtual machines that you rent from AWS.
- **EBS (Elastic Block Store)** – Persistent storage volumes that can be attached to instances.
- **Elastic Load Balancer (ELB)** – Distributes incoming traffic across multiple instances.
- **Auto Scaling Group (ASG)** – Automatically scales instances up or down based on demand.

---

## Customizing EC2 Instances

When creating an EC2 instance, you can configure several aspects:

1. **Operating System**
    - Choose from Linux (most popular), Windows, or even macOS.

2. **Compute Power**
    - Select the number of CPUs and cores depending on workload needs.

3. **Memory (RAM)**
    - Allocate the required amount of random-access memory.

4. **Storage**
    - Choose storage type:
        - **EBS/EFS** (Network-attached)
        - **Instance Store** (Hardware-attached, temporary)

5. **Networking**
    - Configure network interfaces, assign public IPs, and define bandwidth.

6. **Security**
    - Control inbound/outbound traffic using **Security Groups** (acts as a virtual firewall).

---

## Bootstrapping with User Data

You can automate the initial configuration of your EC2 instances using a **User Data script**.

### What is Bootstrapping?

Bootstrapping means running setup commands when the machine first starts.  
The **EC2 User Data script** runs **only once** — at the instance’s first launch.

### Typical Bootstrapping Tasks

- Installing system updates
- Installing software packages
- Downloading files or configurations
- Running initialization scripts

> 🧠 **Note:**  
> The User Data script runs as the **root user**, so all commands have `sudo` privileges.  
> The more commands you add, the longer your instance will take to boot.

---

## Why EC2 Matters

EC2 embodies the power of the cloud — the ability to **rent compute resources on-demand** and scale instantly based on your needs.  
With EC2, you can:
- Launch virtual servers in minutes
- Scale applications automatically
- Only pay for what you use

---

## Summary

| Concept | Description |
|----------|--------------|
| **Service Type** | Infrastructure as a Service (IaaS) |
| **Main Component** | EC2 Instances |
| **Storage Options** | EBS, EFS, Instance Store |
| **Scaling** | Auto Scaling Groups |
| **Load Distribution** | Elastic Load Balancer |
| **Security** | Security Groups |
| **Automation** | EC2 User Data (Bootstrapping) |

---

# 🚀 Launching Your First EC2 Instance on AWS

We'll **launch our first EC2 instance running Amazon Linux** and deploy a simple **web server** using a *User Data* script.

---

## ⚙️ Step 1 — Launch an EC2 Instance

1. Go to the **EC2 Console** → click **Instances** → then **Launch Instances**
2. **Name and Tags**:
   - Name your instance: `My First Instance`
   - Tags are optional, e.g., `Environment=Test`

---

## 🧠 Step 2 — Choose an Amazon Machine Image (AMI)

- Select **Amazon Linux 2 AMI (64-bit x86)**
- This image is **free tier eligible** and maintained by AWS.
- AMI defines the **operating system** your instance will run.

---

## ⚡ Step 3 — Choose Instance Type

- Select **t2.micro** (Free Tier Eligible)
- This provides 1 vCPU and 1 GB of memory
- Ideal for testing and learning

You can compare other instance types if you want more power or newer generations (e.g., `t3.micro`).

---

## 🔑 Step 4 — Create or Select a Key Pair

A **key pair** allows you to securely connect to your EC2 instance via SSH.

- Click **Create Key Pair**
- Name it: `EC2-Tutorial`
- **Key type:** RSA
- **File format:**
   - `.pem` → For Mac, Linux, or Windows 10+
   - `.ppk` → For older Windows versions (for PuTTY)
- Download the file safely — you’ll need it to connect later.

---

## 🌐 Step 5 — Configure Network Settings

- **VPC & Subnet:** Leave default
- **Auto-assign Public IP:** Enabled (so you can access it from the internet)
- **Security Group:** Create a new one (automatically named `launch-wizard-1`)
   - Allow **SSH (port 22)** from anywhere
   - Allow **HTTP (port 80)** from anywhere

This ensures:
- You can connect via SSH
- The world can view your web page

---

## 💾 Step 6 — Configure Storage

- Default volume: **8 GiB gp2 (SSD)**
- Free Tier allows up to **30 GiB**, so leave defaults
- Optionally check “**Delete on Termination**” → enabled by default

---

## 🧰 Step 7 — Add User Data (Bootstrapping Script)

At the bottom of the “Advanced Details” section, find **User Data**.  
Paste the following script (provided in the course):

```bash
#!/bin/bash
yum update -y
yum install -y httpd
systemctl start httpd
systemctl enable httpd
echo "<h1>Hello World from $(hostname -f)</h1>" > /var/www/html/index.html
```

## 🌐 Access

- **Public** IPv4 address → Use this to access your instance (may change on restart)
- **Private** IPv4 address → Used internally within AWS (stays the same)
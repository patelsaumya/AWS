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

---

## 🔌 Step 8 — Connect to Your EC2 Instance via SSH

Once your instance is running, you can connect to it using SSH. There are two main methods:

### Option 1: Local Command Line (SSH)

Use your local terminal or command prompt to connect directly:

**Windows (PowerShell/Command Prompt):**
```bash
ssh -i .\EC2Tutorial.pem ec2-user@<PUBLIC_IP_ADDRESS>
```

**Mac/Linux:**
```bash
ssh -i ~/EC2Tutorial.pem ec2-user@<PUBLIC_IP_ADDRESS>
```

**Notes:**
- Replace `<PUBLIC_IP_ADDRESS>` with your instance's public IPv4 address
- The `.pem` file must be in the current directory (or provide the full path)
- For Amazon Linux, the default username is `ec2-user`
- You may need to set proper permissions on the `.pem` file first

### Option 2: EC2 Instance Connect (AWS Console)

Connect directly from the AWS Management Console without needing SSH keys:

1. Go to **EC2 Console** → **Instances**
2. Select your instance
3. Click **Connect** button
4. Choose **EC2 Instance Connect** tab
5. Click **Connect**

This opens a browser-based terminal session directly in your AWS console.

> 🧠 **Note:**  
> EC2 Instance Connect works without managing SSH keys.

---

## ⛑️ Shared Responsibility Model

### 🔹 AWS Responsibilities

AWS is responsible for:

* **Data centers** – Physical infrastructure and security of all AWS facilities.
* **Physical host isolation** – Ensuring proper isolation on physical hosts (e.g., dedicated hosts).
* **Hardware management** – Replacing faulty hardware when servers fail.
* **Compliance** – Maintaining regulatory compliance for infrastructure and certifications.
* **Virtualization layer** – Managing the hypervisor and virtualization infrastructure.

### 🔹 Customer Responsibilities

You are responsible for:

* **Security Groups** – Defining your own security group rules to control inbound/outbound traffic and access to your EC2 instances.
* **Operating System** – Managing the entire virtual machine, including:
  * OS patches and updates (Windows, Linux, or macOS).
  * OS configuration and hardening.
* **Software & Utilities** – All software and utilities installed on your EC2 instance.
* **IAM Roles & Permissions** – Understanding how to assign IAM roles and ensuring permissions are correctly configured.
* **Data Security** – Making sure data stored on your EC2 instance is secure and properly managed.

> 🧠 **Key Takeaway:**  
> AWS provides the virtual machine infrastructure, but you own and manage everything inside it—from the operating system to the applications and data.
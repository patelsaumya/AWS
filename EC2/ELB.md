# ⚖️ Elastic Load Balancing (ELB)

## 📋 Overview

**Elastic Load Balancing (ELB)** is a managed AWS service that automatically distributes incoming traffic across multiple targets, such as EC2 instances, in multiple Availability Zones. Load balancers help make your applications more elastic and highly available by spreading the load and handling failures gracefully.

---

## 🔍 What is a Load Balancer?

A **load balancer** is a server that forwards internet traffic to multiple servers (called downstream instances). In AWS, these downstream servers are typically EC2 instances, also known as **backend EC2 instances**.

### ⚙️ How It Works

1. **User requests** come to the load balancer (publicly exposed)
2. **Load balancer** directs traffic to one of the available EC2 instances
3. **EC2 instance** processes the request and sends a response back
4. **Different users** get routed to different EC2 instances for load distribution
5. **More users** = **better load distribution** across multiple instances

### 🌐 Example Flow

```
User 1 → Load Balancer → EC2 Instance A → Response
User 2 → Load Balancer → EC2 Instance B → Response  
User 3 → Load Balancer → EC2 Instance C → Response
```

---

## 🎯 Why Use a Load Balancer?

### ✅ Key Benefits

- **Spread load** – Distribute traffic across multiple downstream instances
- **Single point of access** – Expose one DNS hostname for your application
- **Handle failures** – Seamlessly manage failures of downstream instances through health checks
- **SSL termination** – Provide HTTPS for your websites easily
- **Multi-AZ support** – Use across multiple Availability Zones for high availability
- **Health checks** – Automatically detect and route traffic away from unhealthy instances

### 🔒 Additional Features

- **SSL/TLS termination** – Handle encryption/decryption at the load balancer level
- **Sticky sessions** – Route users to the same instance for session consistency
- **High availability** – Built-in redundancy across Availability Zones

---

## 🛠️ Managed Load Balancer Benefits

ELB is a **managed service**, which means:

### 🔹 AWS Handles

- **No server provisioning** – AWS provisions and manages the infrastructure
- **Guaranteed uptime** – AWS guarantees the load balancer will work
- **Upgrades** – AWS takes care of all software upgrades
- **Maintenance** – AWS handles all maintenance tasks
- **High availability** – Built-in redundancy and failover

### 🔹 You Configure

- **Behavior settings** – Configure how the load balancer should behave
- **Target selection** – Choose which instances to route traffic to
- **Health check parameters** – Define how to check instance health

### 💰 Cost Consideration

While you **could** set up your own load balancer on EC2:
- **Less expensive** initially
- **Much more effort** required for maintenance, integration, OS updates, etc.
- **Not recommended** for production environments

---

## 🏷️ Types of Load Balancers

AWS offers **four types** of load balancers:

### 1️⃣ Application Load Balancer (ALB)
### 2️⃣ Network Load Balancer (NLB)  
### 3️⃣ Gateway Load Balancer (GWLB)
### 4️⃣ Classic Load Balancer (Retired)

---

## 🌐 Application Load Balancer (ALB)

### 📋 Overview

**Application Load Balancer** operates at **Layer 7** (Application Layer) and is designed for HTTP/HTTPS traffic.

### 🔑 Key Characteristics

- **Layer 7** – Application layer (HTTP/HTTPS)
- **Protocols** – HTTP, HTTPS, gRPC
- **HTTP routing features** – Advanced routing capabilities
- **Static DNS** – Provides a static URL/hostname

### 🎯 Use Cases

- **Web applications** – HTTP/HTTPS traffic routing
- **Microservices** – Route based on URL paths, headers, query parameters
- **Content-based routing** – Route traffic based on request content
- **Multiple protocols** – Support for HTTP, HTTPS, and gRPC

### 🔄 Architecture

```
Users → ALB (HTTP/HTTPS/gRPC) → EC2 Instances
```

---

## ⚡ Network Load Balancer (NLB)

### 📋 Overview

**Network Load Balancer** operates at **Layer 4** (Transport Layer) and is designed for ultra-high performance with TCP/UDP traffic.

### 🔑 Key Characteristics

- **Layer 4** – Transport layer (TCP/UDP)
- **Ultra-high performance** – Millions of requests per second
- **Static IP** – Provides static IP addresses through Elastic IP
- **Low latency** – Minimal processing overhead

### 🎯 Use Cases

- **High-performance applications** – When you need millions of requests per second
- **TCP/UDP traffic** – Non-HTTP protocols
- **Static IP requirements** – When clients need to connect to specific IP addresses
- **Low latency applications** – Gaming, IoT, real-time applications

### 🔄 Architecture

```
Users → NLB (TCP/UDP) → EC2 Instances
```

---

## 🛡️ Gateway Load Balancer (GWLB)

### 📋 Overview

**Gateway Load Balancer** operates at **Layer 3** (Network Layer) and is designed for routing traffic through third-party security virtual appliances.

### 🔑 Key Characteristics

- **Layer 3** – Network layer (IP packets)
- **GENEVE protocol** – Used for encapsulation
- **Security focus** – Route traffic to security appliances
- **Traffic inspection** – Enable deep packet inspection

### 🎯 Use Cases

- **Firewalls** – Route traffic to firewall instances
- **Intrusion detection** – Deep packet inspection
- **Security appliances** – Third-party security virtual appliances
- **Traffic analysis** – Inspect and analyze network traffic

### 🔄 Architecture

```
Users → GWLB → Security Appliances (EC2) → GWLB → Application
```

The traffic flow:
1. Traffic goes to GWLB
2. GWLB forwards to security appliances on EC2
3. Security appliances analyze/filter traffic
4. Traffic returns to GWLB
5. GWLB forwards to the actual application

---

## 📊 Load Balancer Comparison

| Feature | ALB | NLB | GWLB |
|---------|-----|-----|------|
| **Layer** | 7 (Application) | 4 (Transport) | 3 (Network) |
| **Protocols** | HTTP, HTTPS, gRPC | TCP, UDP | GENEVE (IP) |
| **Performance** | High | Ultra-high (millions req/sec) | High |
| **Static IP** | No (Static DNS) | Yes (Elastic IP) | Yes |
| **Use Case** | Web applications | High-performance apps | Security appliances |
| **Routing** | Content-based | Connection-based | Security inspection |

---

## 📊 Summary

| Concept | Description |
|---------|-------------|
| **Service Type** | Managed load balancing service |
| **Purpose** | Distribute traffic across multiple targets |
| **Benefits** | High availability, fault tolerance, SSL termination |
| **ALB** | Layer 7, HTTP/HTTPS/gRPC, static DNS |
| **NLB** | Layer 4, TCP/UDP, ultra-high performance, static IP |
| **GWLB** | Layer 3, GENEVE, security appliances, traffic inspection |
| **Health Checks** | Automatically detect and avoid unhealthy instances |
| **Multi-AZ** | Built-in high availability across Availability Zones |

---

## 🧪 Hands-On: Creating an Application Load Balancer

### 📋 Overview

Creating an Application Load Balancer with two EC2 instances to demonstrate load balancing and high availability features.

---

### 📝 Step 1: Launch EC2 Instances

#### 1️⃣ Create Two EC2 Instances

1. **Go to EC2 Console** → **Launch Instances**
2. **Configuration Settings:**
   - **Number of instances:** 2
   - **Name:** `My First Instance` (rename second to `My Second Instance`)
   - **AMI:** Amazon Linux 2
   - **Instance type:** t2.micro
   - **Key pair:** Proceed without a key pair (use EC2 Instance Connect if needed)

#### 2️⃣ Configure Security Group

1. **Network settings** → **Select existing security group**
2. **Choose:** `Launch Wizard 1` (allows HTTP and SSH traffic)

#### 3️⃣ Add User Data Script

In **Advanced Details** → **User data**, add this script:

```bash
#!/bin/bash
yum update -y
yum install -y httpd
systemctl start httpd
systemctl enable httpd
echo "<h1>Hello World from $(hostname -f)</h1>" > /var/www/html/index.html
```

#### 4️⃣ Launch and Test Instances

1. **Launch instances** and wait for them to be ready
2. **Test each instance:**
   - Copy the **Public IPv4 address** of first instance
   - Visit the URL in browser → Should see "Hello World from [instance-name]"
   - Repeat for second instance

> 💡 **Expected Result:** Two different URLs, each showing "Hello World" with different instance names

---

### 📝 Step 2: Create Application Load Balancer

#### 1️⃣ Navigate to Load Balancers

1. **EC2 Console** → **Load Balancers** → **Create Load Balancer**
2. **Choose:** **Application Load Balancer**

> 📚 **Quick Review:**
> - **ALB:** HTTP/HTTPS traffic (Layer 7)
> - **NLB:** TCP/UDP, ultra-high performance (Layer 4)
> - **GWLB:** Security, intrusion detection, firewalls (Layer 3)

#### 2️⃣ Configure Basic Settings

1. **Name:** `DemoALB`
2. **Scheme:** Internet-facing
3. **IP address type:** IPv4

#### 3️⃣ Network Mapping

1. **Deploy in all available Availability Zones**
2. **Select all subnets** for high availability

#### 4️⃣ Create Security Group for ALB

1. **Create new security group:**
   - **Name:** `demo-sg-load-balancer`
   - **Description:** `Allow HTTP into ALB`
   - **Inbound rules:** HTTP (port 80) from anywhere (0.0.0.0/0)
   - **Outbound rules:** Leave default

2. **Apply the new security group** to ALB (remove default)

---

### 📝 Step 3: Create Target Group

#### 1️⃣ Create Target Group

1. **Listeners and routing** → **Create target group**
2. **Configuration:**
   - **Target type:** Instances
   - **Name:** `demo-tg-alb`
   - **Protocol:** HTTP
   - **Port:** 80
   - **HTTP version:** HTTP 1

#### 2️⃣ Configure Health Checks

- **Health check path:** `/` (default)
- **Keep all other settings** as default

#### 3️⃣ Register Targets

1. **Select both EC2 instances**
2. **Port:** 80
3. **Click:** "Include as pending below"
4. **Create target group**

---

### 📝 Step 4: Complete ALB Setup

#### 1️⃣ Link Target Group to ALB

1. **Go back to ALB creation page**
2. **Refresh** the target group dropdown
3. **Select:** `demo-tg-alb`
4. **Create load balancer**

#### 2️⃣ Wait for Provisioning

- **Status:** Provisioning → Active (takes a few minutes)

---

### 📝 Step 5: Test Load Balancing

#### 1️⃣ Test Basic Load Balancing

1. **Copy the ALB DNS name** from the load balancer details
2. **Paste into browser** and visit the URL
3. **Refresh the page multiple times**

> ✅ **Expected Result:** The instance name in "Hello World from [instance-name]" should alternate between your two instances, proving load balancing is working.

#### 2️⃣ Verify Target Health

1. **Go to Target Groups** → **Select** `demo-tg-alb`
2. **Targets tab** → Both instances should show **"Healthy"** status

---

### 📝 Step 6: Test High Availability (Failover)

#### 1️⃣ Simulate Instance Failure

1. **Go to EC2 Instances**
2. **Select first instance** → **Instance State** → **Stop Instance**
3. **Wait 30 seconds**

#### 2️⃣ Check Target Group Status

1. **Go to Target Group** → **Targets tab**
2. **Refresh** the page
3. **First instance** should now show **"Unused"** or **"Unhealthy"**

#### 3️⃣ Test Load Balancer Response

1. **Go back to ALB URL**
2. **Refresh multiple times**

> ✅ **Expected Result:** All traffic now goes to the remaining healthy instance. The load balancer automatically stopped sending traffic to the failed instance.

#### 4️⃣ Test Instance Recovery

1. **Start the stopped instance** again
2. **Wait for it to boot up** (2-3 minutes)
3. **Check target group** → Instance should show **"Initial"** then **"Healthy"**
4. **Test ALB URL** → Traffic should now balance between both instances again

---

## 🎯 Key Takeaways

- **ELB is a managed service** – AWS handles all infrastructure, maintenance, and upgrades
- **Three active load balancer types** – ALB (Layer 7), NLB (Layer 4), GWLB (Layer 3)
- **ALB** – Use for HTTP/HTTPS applications with advanced routing features
- **NLB** – Use for ultra-high performance TCP/UDP applications
- **GWLB** – Use for routing traffic through security appliances and firewalls
- **Health checks** automatically route traffic away from failed instances
- **Multi-AZ deployment** provides high availability and fault tolerance
- **Classic Load Balancer** was retired in 2023 and is no longer relevant
- **Choose based on protocol, performance requirements, and use case**

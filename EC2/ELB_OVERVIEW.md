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

> ⚠️ **Note:** Classic Load Balancer was retired in 2023 and is no longer relevant for exams.

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

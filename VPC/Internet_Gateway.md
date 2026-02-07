# 🌐 Internet Gateway (IGW)

## 📋 Overview

**Internet Gateway (IGW)** is a horizontally scaled, redundant, and highly available VPC component that enables communication between resources in your VPC and the internet.

---

## 🔑 Key Characteristics

- **VPC-level resource** – One Internet Gateway per VPC
- **Managed by AWS** – Fully managed, no maintenance required
- **Highly available** – Redundant and horizontally scaled
- **Two-way traffic** – Enables both inbound and outbound internet traffic
- **Public IP translation** – Translates between public and private IP addresses

---

## 🏗️ How It Works

### **Public Subnet Internet Access**

1. **EC2 instance** in public subnet needs internet access
2. **Route table** has route: `0.0.0.0/0 → Internet Gateway`
3. **Internet Gateway** provides:
   - **Outbound:** Private IP → Public IP translation
   - **Inbound:** Public IP → Private IP translation
4. **Direct connectivity** – Resources can communicate with internet

### **Architecture**

```
Internet
    ↕
Internet Gateway (VPC-level)
    ↕
Route Table (0.0.0.0/0 → IGW)
    ↕
Public Subnet
    ↕
EC2 Instance
```

---

## 🔧 Configuration

### **Attach to VPC**

- **One IGW per VPC** – Attach Internet Gateway to your VPC
- **Region-specific** – Internet Gateway is created in a specific region

### **Route Table Configuration**

- **Public subnet route table** must have:
  - Route: `0.0.0.0/0` → `Internet Gateway`
- **This route makes subnet public** – Without it, subnet is private

---

## 🎯 Key Takeaways

✅ **Internet Gateway = VPC-level resource** for internet connectivity

✅ **One per VPC** – Attach one Internet Gateway to your VPC

✅ **Public subnet requirement** – Public subnets need route to Internet Gateway

✅ **Route table:** `0.0.0.0/0 → Internet Gateway` makes subnet public

✅ **Two-way traffic** – Enables both inbound and outbound internet access

✅ **Fully managed** – AWS manages availability and scaling

✅ **IP translation** – Translates between private and public IP addresses

✅ **Use case:** Enable public internet access for resources in public subnets

---


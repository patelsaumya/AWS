# 💻 AWS Client VPN

## 📋 Overview

**AWS Client VPN** allows you to connect your computer privately to your AWS VPC using OpenVPN. Once connected, you can access resources in your VPC as if you were on the VPC network.

---

## 🔑 Key Characteristics

- **OpenVPN protocol** – Uses OpenVPN to establish connection
- **Private access** – Access VPC resources using private IPs
- **Over internet** – Connection goes over public internet (encrypted)
- **Client-based** – VPN client installed on your computer
- **On-premises access** – Can also access on-premises resources if Site-to-Site VPN is configured

---

## 🏗️ How It Works

### **Connection Flow**

```
Your Computer
├── Client VPN (OpenVPN)
    ↕ (Over Public Internet)
AWS VPC
└── Client VPN Endpoint
    └── Private Subnets
        └── EC2 Instances (Private IPs)
```

### **With Site-to-Site VPN**

```
Your Computer
├── Client VPN
    ↕
AWS VPC
├── Client VPN Endpoint
└── Site-to-Site VPN
    ↕
On-Premises Data Center
```

**Result:** Your computer can access both VPC resources and on-premises resources privately.

---

## 🎯 Use Cases

- **Access private EC2 instances** – Connect to EC2 instances using their private IP addresses
- **Remote access** – Access VPC resources from anywhere
- **On-premises access** – Access on-premises servers if Site-to-Site VPN is configured
- **Private network access** – Access resources as if you were on the VPC network

---

## 🎯 Key Takeaways

✅ **AWS Client VPN = Private connection** from your computer to VPC using OpenVPN

✅ **Characteristics:**
- **OpenVPN protocol** – Uses OpenVPN
- **Over internet** – Connection goes over public internet (encrypted)
- **Private access** – Access resources using private IPs
- **Client-based** – VPN client installed on your computer

✅ **Use cases:**
- Access EC2 instances using **private IP addresses**
- Access VPC resources from anywhere
- Access **on-premises resources** (if Site-to-Site VPN configured)

✅ **Architecture:**
- Your Computer → Client VPN → Internet → Client VPN Endpoint → VPC
- With Site-to-Site VPN: Also access on-premises data center

✅ **Benefit:** Access VPC resources privately as if you were on the VPC network yourself

---


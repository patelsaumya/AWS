# 🔐 Site-to-Site VPN

## 📋 Overview

**Site-to-Site VPN** connects your on-premises data center to your AWS VPC over the **public internet** with encrypted communication. It's quick to set up (about 5 minutes) but uses public internet.

---

## 🔑 Key Characteristics

- **Encrypted connection** – Traffic encrypted over public internet
- **Public internet** – Connection goes over public internet (encrypted)
- **Quick setup** – Can be established in about 5 minutes
- **Limited bandwidth** – Bandwidth limited by internet connection
- **Cost-effective** – Lower cost than Direct Connect

---

## 🏗️ Components

### **On-Premises Side**

- **Customer Gateway (CGW)** – Physical device or software application on your side

### **AWS Side**

- **Virtual Private Gateway (VGW)** – AWS-managed VPN gateway attached to your VPC

### **Connection**

- **Site-to-Site VPN** – Encrypted connection between CGW and VGW over public internet

---

## 🏛️ Architecture

```
On-Premises Data Center
├── Customer Gateway (CGW)
    ↕ (Encrypted over Public Internet)
AWS VPC
├── Virtual Private Gateway (VGW)
└── Private Subnets
    └── EC2 Instances
```

---

## 🎯 Use Cases

- **Hybrid cloud** – Connect corporate data center to AWS VPC
- **Quick connectivity** – Need connection established quickly
- **Cost-sensitive** – Lower cost than Direct Connect
- **Temporary connections** – Short-term or testing scenarios

---

## ⚖️ Site-to-Site VPN vs. Direct Connect

| Factor | Site-to-Site VPN | Direct Connect |
|--------|------------------|----------------|
| **Network** | Public internet (encrypted) | Private network |
| **Setup time** | ~5 minutes | At least 1 month |
| **Bandwidth** | Limited | High, dedicated |
| **Cost** | Lower | Higher |
| **Security** | Encrypted (public internet) | Private and secure |
| **Reliability** | Depends on internet | More reliable |

---

## 🎯 Key Takeaways

✅ **Site-to-Site VPN = Encrypted connection** over public internet

✅ **Components:**
- **Customer Gateway (CGW)** – On-premises side
- **Virtual Private Gateway (VGW)** – AWS side
- **Site-to-Site VPN** – Connection between them

✅ **Characteristics:**
- **Quick setup** – ~5 minutes
- **Public internet** – Encrypted traffic over internet
- **Limited bandwidth** – Depends on internet connection
- **Cost-effective** – Lower cost than Direct Connect

✅ **Use when:**
- Need connection **quickly**
- **Cost-sensitive**
- Can accept **public internet** (encrypted)
- **Limited bandwidth** is acceptable

---


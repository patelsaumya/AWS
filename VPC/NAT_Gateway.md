# 🌐 NAT Gateway

## 📋 Overview

**NAT Gateway (Network Address Translation Gateway)** is a managed AWS service that allows resources in **private subnets** to access the internet while remaining private (not accessible from the internet).

---

## 🔑 Key Characteristics

- **Managed by AWS** – Fully managed, no maintenance required
- **High availability** – Redundant within a single Availability Zone
- **Elastic IP required** – NAT Gateway uses an Elastic IP address
- **Subnet placement** – Must be created in a **public subnet**
- **Outbound only** – Allows outbound internet traffic (no inbound from internet)
- **Scalable** – Automatically scales up to 45 Gbps

---

## 🏗️ How It Works

### **Private Subnet Internet Access**

1. **EC2 instance** in private subnet needs internet access (e.g., OS updates, downloads)
2. **Route table** has route: `0.0.0.0/0 → NAT Gateway`
3. **NAT Gateway** (in public subnet) forwards traffic to [Internet Gateway](Internet_Gateway.md)
4. **Internet Gateway** provides internet connectivity
5. **Response traffic** – Returns through same path (NAT Gateway maintains connection state)

### **Architecture**

```
Internet
    ↕
Internet Gateway
    ↕
NAT Gateway (in Public Subnet)
    ↕
Route Table (0.0.0.0/0 → NAT Gateway)
    ↕
Private Subnet
    ↕
EC2 Instance (remains private)
```

---

## 🔧 Configuration

### **Create NAT Gateway**

1. **Select public subnet** – NAT Gateway must be in a public subnet
2. **Allocate Elastic IP** – NAT Gateway requires an Elastic IP address
3. **Wait for creation** – Takes a few minutes to become available

### **Route Table Configuration**

- **Private subnet route table** must have:
  - Route: `0.0.0.0/0` → `NAT Gateway`
- **Public subnet route table** (where NAT Gateway resides):
  - Route: `0.0.0.0/0` → `Internet Gateway`

### **Multi-AZ Setup**

- **One NAT Gateway per AZ** – For high availability, create NAT Gateway in each AZ
- **Route private subnets** – Each AZ's private subnet routes to its own NAT Gateway

---

## 💰 Pricing

- **Per hour:** ~$0.045/hour (varies by region)
- **Data processing:** ~$0.045/GB (data processed by NAT Gateway)
- **Elastic IP:** Included (no additional charge when attached to NAT Gateway)

---

## 🔄 NAT Gateway vs. NAT Instance

| Feature | NAT Gateway | NAT Instance |
|---------|-------------|--------------|
| **Management** | AWS-managed | Self-managed |
| **Availability** | Highly available (within AZ) | Single instance (create in each AZ) |
| **Maintenance** | No maintenance | OS updates, patches required |
| **Scaling** | Automatic (up to 45 Gbps) | Manual (instance type limits) |
| **Cost** | Pay per hour + data processing | EC2 instance cost |
| **Bandwidth** | Up to 45 Gbps | Depends on instance type |

---

## 🎯 Key Takeaways

✅ **NAT Gateway = Managed service** for private subnet internet access

✅ **Placement:** Must be created in a **public subnet**

✅ **Elastic IP required** – NAT Gateway uses an Elastic IP address

✅ **Private subnet route:** `0.0.0.0/0 → NAT Gateway` enables internet access

✅ **Outbound only** – Allows outbound traffic, resources remain private

✅ **Architecture:** Private Subnet → NAT Gateway → Internet Gateway → Internet

✅ **High availability:** Create one NAT Gateway per AZ for multi-AZ deployments

✅ **Use case:** Allow private subnet resources (databases, app servers) to access internet for updates/downloads while remaining secure

✅ **NAT Gateway vs. NAT Instance:** Prefer NAT Gateway (managed, scalable, highly available)

---


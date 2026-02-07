# 🌐 Subnets

## 📋 Overview

**Subnets** are partitions of your VPC network, each associated with one **Availability Zone**. Subnets enable you to organize resources and control internet accessibility.

---

## 🏗️ Subnet Types

### **Public Subnet**

- **Internet-accessible** – Resources in public subnet can be reached from the internet
- **Direct internet connectivity** – Has route to [Internet Gateway](Internet_Gateway.md)
- **Route table** – Contains route `0.0.0.0/0 → Internet Gateway`
- **Use cases:**
  - EC2 instances (web servers)
  - Load Balancers
  - NAT Gateways/NAT Instances

### **Private Subnet**

- **Not internet-accessible** – Resources cannot be reached from the internet
- **Internet access via NAT** – Can access internet through [NAT Gateway](NAT_Gateway.md) or NAT Instance
- **Route table** – Contains route `0.0.0.0/0 → NAT Gateway` (not Internet Gateway)
- **Use cases:**
  - Databases (RDS, DynamoDB)
  - Application servers
  - Internal services (more secure)

---

## 🔑 Key Characteristics

### **Availability Zone Association**

- **One AZ per subnet** – Each subnet is associated with exactly one Availability Zone
- **Multi-AZ deployment** – Create subnets in multiple AZs for high availability
- **Cannot span AZs** – A subnet cannot exist across multiple Availability Zones

### **CIDR Blocks**

- **Subnet IP range** – Each subnet has its own CIDR block (subset of VPC CIDR)
- **Example:**
  - VPC: `10.0.0.0/16` (65,536 IPs)
  - Public Subnet AZ1: `10.0.1.0/24` (256 IPs)
  - Private Subnet AZ1: `10.0.2.0/24` (256 IPs)

### **Route Tables**

- **Traffic routing** – Route tables define how traffic flows
- **Subnet association** – Each subnet must be associated with a route table
- **Default route table** – VPC has a default route table (can be modified)
- **Custom route tables** – Create separate route tables for public/private subnets

---

## 🏛️ Architecture Example

```
VPC (10.0.0.0/16)
├── AZ 1
│   ├── Public Subnet (10.0.1.0/24)
│   │   └── Route Table: 0.0.0.0/0 → Internet Gateway
│   └── Private Subnet (10.0.2.0/24)
│       └── Route Table: 0.0.0.0/0 → NAT Gateway
└── AZ 2
    ├── Public Subnet (10.0.3.0/24)
    │   └── Route Table: 0.0.0.0/0 → Internet Gateway
    └── Private Subnet (10.0.4.0/24)
        └── Route Table: 0.0.0.0/0 → NAT Gateway
```

---

## 🎯 Key Takeaways

✅ **Subnet = Network partition** within VPC, associated with one Availability Zone

✅ **Public Subnet:**
- Internet-accessible
- Route to Internet Gateway
- Use for: EC2, Load Balancers, NAT Gateways

✅ **Private Subnet:**
- Not internet-accessible
- Route to NAT Gateway (for outbound internet)
- Use for: Databases, internal services (more secure)

✅ **Route Tables** – Define internet connectivity (Internet Gateway = public, NAT Gateway = private)

✅ **Multi-AZ** – Create subnets in multiple AZs for high availability

✅ **CIDR blocks** – Subnets have smaller CIDR blocks within VPC CIDR range

---


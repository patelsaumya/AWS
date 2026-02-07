# 🔒 Network ACL & Security Groups

## 📋 Overview

**Network ACL (NACL)** and **Security Groups** are two layers of network security in VPC. NACL operates at the **subnet level**, while Security Groups operate at the **ENI level**.

---

## 🛡️ Network ACL (NACL - Network Access Control List)

### **Key Characteristics**

- **Subnet-level firewall** – Controls traffic to and from the subnet
- **First line of defense** – Filters traffic before it reaches EC2 instances
- **ALLOW and DENY rules** – Supports both allow and deny rules
- **Stateless** – Return traffic must be explicitly allowed by rules
- **IP addresses only** – Rules can only reference IP addresses (not security groups)

### **How It Works**

```
Internet
    ↓
NACL (Subnet Level) ← Filters traffic in/out of subnet
    ↓
EC2 Instance
```

- **Inbound rules** – Control traffic entering the subnet
- **Outbound rules** – Control traffic leaving the subnet
- **Rule evaluation** – Rules are evaluated in order (lowest rule number first)
- **Default NACL** – VPC has a default NACL that allows all traffic

---

## 🛡️ Security Groups

### **Key Characteristics**

- **ENI-level firewall** – Controls traffic to and from Elastic Network Interfaces (attached to EC2 instances, Lambda, RDS, etc.)
- **Second line of defense** – Applied after NACL filtering
- **ALLOW rules only** – Security groups only support ALLOW rules
- **Stateful** – Return traffic is automatically allowed (regardless of rules)
- **IP addresses and Security Groups** – Rules can reference IP addresses or other security groups

### **How It Works**

```
NACL (Subnet Level)
    ↓
Security Group (Instance Level) ← Controls traffic to/from EC2
    ↓
EC2 Instance
```

- **Inbound rules** – Control traffic entering the instance
- **Outbound rules** – Control traffic leaving the instance
- **Default deny** – All traffic denied by default (must explicitly allow)

---

## 📊 Comparison Table

| Feature | Security Group | Network ACL |
|---------|---------------|-------------|
| **Level** | ENI level | Subnet level |
| **Rules** | ALLOW only | ALLOW and DENY |
| **Statefulness** | Stateful (return traffic auto-allowed) | Stateless (return traffic must be explicitly allowed) |
| **References** | IP addresses, Security Groups | IP addresses only |
| **Evaluation** | All rules evaluated | Rules evaluated in order (lowest number first) |
| **Default** | Deny all (must allow explicitly) | Default NACL allows all |

---

## 🏗️ Architecture Example

```
Internet
    ↓
NACL (Subnet Level)
    ├── Rule 100: ALLOW all traffic (0.0.0.0/0)
    └── Rule *: DENY all (default)
    ↓
Security Group (Instance Level)
    ├── Inbound: ALLOW SSH (22) from 10.0.0.0/16
    └── Outbound: ALLOW all (0.0.0.0/0)
    ↓
EC2 Instance
```

**Traffic Flow:**
1. **NACL** filters traffic at subnet level
2. **Security Group** filters traffic at ENI level
3. If both allow, traffic reaches EC2 instance

---

## 🛠️ Hands-On

### **Step 1: View Security Groups**

1. Go to **VPC Console** → **Security** → **Security Groups**
   - Or view from **EC2 Console** → **Security Groups**
2. **View security groups** – All security groups created in the VPC
3. **Click on a security group** (e.g., `launch-wizard-7`)
4. **View rules:**
   - **Inbound rules** – Traffic allowed into instances
   - **Outbound rules** – Traffic allowed out of instances

### **Step 2: View Network ACLs**

1. Go to **VPC Console** → **Security** → **Network ACLs**
2. **Default NACL** – VPC has a default NACL associated with all subnets
3. **View subnet associations:**
   - Click on default NACL
   - See **Subnet associations** (e.g., 3 subnets)
   - Network ACLs are **subnet-level** (not ENI-level)

### **Step 3: Examine Default NACL Rules**

1. **Inbound rules:**
   - **Rule 100:** ALLOW all traffic (`0.0.0.0/0`) on all ports
   - **Rule * (last):** DENY all (default deny)
   - **Result:** All traffic allowed (rule 100 matches first)

2. **Outbound rules:**
   - **Rule 100:** ALLOW all traffic (`0.0.0.0/0`) on all ports
   - **Rule * (last):** DENY all (default deny)
   - **Result:** All traffic allowed

### **Step 4: Understand Rule Evaluation**

1. **Rule order matters:**
   - Rules evaluated from **lowest number to highest**
   - First matching rule applies
   - `*` rule is evaluated last (default deny)

2. **Example modification:**
   - **Remove rule 100** (allow all)
   - **Add rule 200:** ALLOW HTTPS (443) from `0.0.0.0/0`
   - **Result:** Only HTTPS traffic allowed, everything else denied

### **Key Observations**

- **NACL = Subnet level** – One NACL can be associated with multiple subnets
- **Security Group = ENI level** – Each ENI can have one or more security groups
- **Default NACL** – Allows all traffic (rule 100 allows all)
- **Default Security Group** – Denies all (must explicitly allow)
- **Rule evaluation:** NACL rules evaluated in order, Security Group rules all evaluated
- **Statefulness:** Security Groups are stateful (return traffic auto-allowed), NACLs are stateless

---

## 🎯 Key Takeaways

✅ **Two layers of defense:**
- **NACL (Network ACL)** – Subnet-level firewall (first line)
- **Security Group** – ENI-level firewall (second line)

✅ **NACL:**
- **Subnet level** – Controls traffic to/from subnet
- **ALLOW and DENY rules** – Supports both
- **Stateless** – Return traffic must be explicitly allowed
- **IP addresses only** – Cannot reference security groups

✅ **Security Group:**
- **ENI level** – Controls traffic to/from Elastic Network Interface (attached to EC2, Lambda, RDS, etc.)
- **ALLOW rules only** – Cannot deny (default deny)
- **Stateful** – Return traffic automatically allowed
- **IP addresses and Security Groups** – Can reference other security groups

✅ **Default behavior:**
- **Default NACL** – Allows all traffic
- **Default Security Group** – Denies all traffic (must allow explicitly)

✅ **Rule evaluation:**
- **NACL** – Rules evaluated in order (lowest number first)
- **Security Group** – All rules evaluated

---


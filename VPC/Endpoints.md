# 🔌 VPC Endpoints

## 📋 Overview

**VPC Endpoints** allow you to connect to AWS services privately using AWS's private network instead of the public internet. This provides better security and lower latency.

---

## 🔑 Key Characteristics

- **Private connectivity** – Connect to AWS services without going over public internet
- **Better security** – Traffic stays on AWS private network
- **Lower latency** – No network hops through public internet
- **Two types:** Gateway Endpoint and Interface Endpoint

---

## 🏗️ Endpoint Types

### **Gateway Endpoint**

- **Services:** Amazon S3 and DynamoDB **only**
- **Type:** Gateway (not interface)
- **Free** – No additional charges
- **Route table** – Automatically adds route to route table
- **No ENI** – Does not use Elastic Network Interface

### **Interface Endpoint**

- **Services:** All other AWS services (CloudWatch, EC2, etc.)
- **Type:** Interface (uses ENI)
- **Pricing:** Pay per hour and per GB of data processed
- **ENI** – Uses Elastic Network Interface in your subnet
- **Private IP** – Gets a private IP address in your subnet

---

## 🏛️ Architecture Example

### **Gateway Endpoint (S3/DynamoDB)**

```
EC2 Instance (Private Subnet)
    ↓
Gateway Endpoint
    ↓
Amazon S3 / DynamoDB (Private AWS Network)
```

### **Interface Endpoint (Other Services)**

```
EC2 Instance (Private Subnet)
    ↓
Interface Endpoint (ENI in Subnet)
    ↓
AWS Service (e.g., CloudWatch) (Private AWS Network)
```

---

## 🎯 Use Cases

### **Private Subnet Access**

- **EC2 in private subnet** needs to access S3, DynamoDB, CloudWatch, etc.
- **Without endpoint:** Traffic goes through NAT Gateway → Internet → AWS service
- **With endpoint:** Traffic goes directly through AWS private network

### **Security Benefits**

- **No public internet** – Traffic never leaves AWS network
- **Reduced attack surface** – No exposure to public internet
- **Compliance** – Meets requirements for private connectivity

### **Performance Benefits**

- **Lower latency** – Direct connection through AWS network
- **No network hops** – Avoids public internet routing
- **Consistent performance** – Predictable network path

---

## 🔧 Configuration

### **Create Gateway Endpoint**

1. Go to **VPC Console** → **Endpoints** → **Create endpoint**
2. **Service category:** AWS services
3. **Service name:** Search for "S3" or "DynamoDB"
4. **Type:** Gateway (only option for S3/DynamoDB)
5. **VPC:** Select your VPC
6. **Route tables:** Select route tables to add route automatically
7. **Policy:** Optional resource policy

### **Create Interface Endpoint**

1. Go to **VPC Console** → **Endpoints** → **Create endpoint**
2. **Service category:** AWS services
3. **Service name:** Search for service (e.g., "CloudWatch", "EC2")
4. **Type:** Interface (default for most services)
5. **VPC:** Select your VPC
6. **Subnets:** Select subnets (ENI created in each subnet)
7. **Security groups:** Select security groups for ENI
8. **Policy:** Optional resource policy

---

## 🛠️ Hands-On

### **Step 1: View Available Services**

1. Go to **VPC Console** → **Endpoints** → **Create endpoint**
2. **Service category:** AWS services (default)
3. **Scroll through service list** – See all available services
4. **Most services** have Interface Endpoint option

### **Step 2: Create Gateway Endpoint (S3/DynamoDB)**

1. **Search for "S3"** or **"DynamoDB"**
2. **Two options available:**
   - **Interface endpoint** – Available
   - **Gateway endpoint** – Available (only for S3 and DynamoDB)
3. **Select Gateway endpoint:**
   - **VPC:** Select your VPC
   - **Route tables:** Select route tables (route added automatically)
   - **Policy:** Optional
4. **Create endpoint**

### **Step 3: Create Interface Endpoint (Other Services)**

1. **Search for service** (e.g., "EC2", "CloudWatch")
2. **Only Interface endpoint** available (no Gateway option)
3. **Configure:**
   - **VPC:** Select your VPC
   - **Subnets:** Select subnets (ENI created in each)
   - **Security groups:** Select security groups
   - **Policy:** Optional
4. **Create endpoint**

### **Key Observations**

- **Gateway Endpoint:** Only S3 and DynamoDB have this option
- **Interface Endpoint:** Available for almost all AWS services
- **S3 and DynamoDB:** Have both Gateway and Interface endpoint options
- **Other services:** Only have Interface endpoint option
- **Gateway = Free:** Gateway endpoints have no additional charges
- **Interface = Paid:** Interface endpoints charge per hour and per GB

---

## 🎯 Key Takeaways

✅ **VPC Endpoints = Private connectivity** to AWS services using AWS private network

✅ **Benefits:**
- **Better security** – No public internet exposure
- **Lower latency** – Direct AWS network connection
- **No network hops** – Avoids public internet routing

✅ **Two types:**
- **Gateway Endpoint** – S3 and DynamoDB only, free, uses route table
- **Interface Endpoint** – All other services, paid, uses ENI

✅ **Configuration:**
- **Gateway:** Select VPC and route tables (route added automatically)
- **Interface:** Select VPC, subnets, and security groups (ENI created)

✅ **Use case:** Allow private subnet resources to access AWS services without going through public internet or NAT Gateway

---


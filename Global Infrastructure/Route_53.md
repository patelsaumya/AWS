# 🌐 Amazon Route 53

## 📋 Overview

**Amazon Route 53** is a managed DNS (Domain Name System) service that helps clients find the right servers through URLs. Route 53 is essential for deploying global applications and routing traffic efficiently.

---

## 🔍 What is DNS?

**DNS (Domain Name System)** is like a phone book - a collection of rules and records that map domain names to IP addresses, allowing clients to find servers through human-readable URLs instead of numeric IP addresses.

---

## 📝 Common DNS Record Types

### 1. **A Record**
- **Maps:** Domain name to IPv4 address
- **Example:** `www.google.com` → `142.250.191.14`

### 2. **AAAA Record**
- **Maps:** Domain name to IPv6 address
- **Example:** `www.google.com` → `2607:f8b0:4004:c1b::65`

### 3. **CNAME Record**
- **Maps:** Hostname to another hostname
- **Example:** `www.google.com` → `google.com`

### 4. **Alias Record** (AWS-Specific)
- **Maps:** Hostname to AWS resource
- **Works with:** ELB, CloudFront, S3, RDS, and other AWS resources
- **Benefit:** Native AWS integration, no additional cost

---

## 🏗️ How DNS Works (High-Level)

### 📊 DNS Request Flow

```
Web Browser → DNS Query (myapp.mydomain.com) → Route 53 → IP Address Response → Web Browser → Application Server → HTTP Response
```

**Step-by-step:**
1. **Web browser** makes DNS request for `myapp.mydomain.com`
2. **Route 53** receives the DNS query
3. **Route 53** looks up the A Record and returns the IP address
4. **Web browser** uses the IP address to connect to the application server
5. **Application server** responds with HTTP content

---

## 🎯 Route 53 Routing Policies

Routing policies determine how Route 53 responds to DNS queries. Choose the right policy based on your use case.

### 1. **Simple Routing Policy**
- **Health checks:** ❌ No
- **Use case:** Basic routing to a single resource
- **How it works:** Returns one IP address or multiple IP addresses (random selection)
- **Example:** Single application server or multiple servers with equal priority

### 2. **Weighted Routing Policy**
- **Health checks:** ✅ Yes (optional)
- **Use case:** Distribute traffic across multiple instances
- **How it works:** Assign weights to instances (e.g., 70%, 20%, 10%)
- **Traffic distribution:** Route 53 distributes traffic based on assigned weights
- **Example:** 70% traffic to instance 1, 20% to instance 2, 10% to instance 3
- **Benefit:** Effective load balancing at DNS level

### 3. **Latency Routing Policy**
- **Health checks:** ✅ Yes (optional)
- **Use case:** Minimize latency by routing to closest server
- **How it works:** 
  - Route 53 determines user location
  - Routes to the server with lowest latency for that user
- **Example:** User in US → California server, User in Asia → Australia server
- **Benefit:** Optimizes user experience by reducing latency

### 4. **Failover Routing Policy**
- **Health checks:** ✅ Yes (required)
- **Use case:** Disaster recovery and high availability
- **How it works:**
  - Route 53 performs health checks on primary instance
  - If primary fails → automatically routes to failover instance
- **Architecture:** Primary instance + Failover instance
- **Benefit:** Automatic failover for disaster recovery

---

## 📊 Routing Policies Comparison

| Routing Policy | Health Checks | Primary Use Case | Key Feature |
|----------------|---------------|------------------|-------------|
| **Simple** | ❌ No | Basic routing | Single or multiple IPs |
| **Weighted** | ✅ Yes (optional) | Traffic distribution | Load balancing by weight |
| **Latency** | ✅ Yes (optional) | Minimize latency | Route to closest server |
| **Failover** | ✅ Yes (required) | Disaster recovery | Automatic failover |

---

## 🧪 Hands-On: Latency-Based Routing with Route 53

### 📋 Overview

This hands-on demonstrates how Route 53's Latency routing policy routes users to the closest server based on their location, minimizing latency.

---

### 📝 Step 1: Register a Domain (Optional)

1. **Navigate to Route 53 Console** → **Registered domains**
2. **Register a domain** (costs ~$12/year)
   - Choose an available domain name
   - Complete registration information
   - Wait 10-15 minutes for processing

> ⚠️ **Note:** Domain registration costs money. You can skip this step and watch the demonstration.

---

### 📝 Step 2: Access Hosted Zone

1. **Go to Route 53 Console** → **Hosted zones**
2. **Verify hosted zone created** automatically for your domain
3. **Note:** This is where DNS records will be created

---

### 📝 Step 3: Create EC2 Instances in Different Regions

#### 1️⃣ Create Instance in Ireland (eu-west-1)

1. **Switch to Ireland region** (eu-west-1)
2. **Launch EC2 instance:**
   - **Instance type:** t2.micro
   - **Security group:** Allow HTTP traffic from anywhere
   - **User data:**
     ```bash
     #!/bin/bash
     yum update -y
     yum install -y httpd
     systemctl start httpd
     systemctl enable httpd
     echo "<h1>Hello world from Ireland</h1>" > /var/www/html/index.html
     ```
3. **Note the public IPv4 address** of the instance
4. **Test:** Access the IP address in browser → Should see "Hello world from Ireland"

#### 2️⃣ Create Instance in US West 2 (us-west-2)

1. **Switch to US West 2 region** (us-west-2)
2. **Launch EC2 instance:**
   - **Instance type:** t2.micro
   - **Security group:** Allow HTTP traffic from anywhere
   - **User data:**
     ```bash
     #!/bin/bash
     yum update -y
     yum install -y httpd
     systemctl start httpd
     systemctl enable httpd
     echo "<h1>Hello world from the US</h1>" > /var/www/html/index.html
     ```
3. **Note the public IPv4 address** of the instance
4. **Test:** Access the IP address in browser → Should see "Hello world from the US"

---

### 📝 Step 4: Create A Records with Latency Routing

1. **Go to Route 53 Console** → **Hosted zones** → Your domain
2. **Create first A record:**
   - **Record name:** `www`
   - **Record type:** A
   - **Value:** Ireland instance IPv4 address (remove `http://` if copied)
   - **Routing policy:** Latency-based routing
   - **Region:** EU (Ireland) - eu-west-1
   - **Record ID:** "My instance from Ireland"
3. **Create second A record:**
   - **Record name:** `www`
   - **Record type:** A
   - **Value:** US West 2 instance IPv4 address
   - **Routing policy:** Latency-based routing
   - **Region:** US West (Oregon) - us-west-2
   - **Record ID:** "My US Instance"
4. **Create records**

---

### 📝 Step 5: Test Latency-Based Routing

#### 1️⃣ Test from Your Location

1. **Open browser** → Navigate to `www.yourdomain.com`
2. **Expected result:** See "Hello world from Ireland" (or closest region)
3. **Refresh:** Should remain on the same instance

#### 2️⃣ Test with VPN (Different Location)

1. **Connect to VPN** in a different country (e.g., United States)
2. **Open private/incognito window**
3. **Navigate to** `www.yourdomain.com`
4. **Expected result:** See "Hello world from the US" (closest to VPN location)

> ✅ **Success:** Route 53 automatically routes to the instance with lowest latency based on user location!

---

### 🔍 Key Observations

**Latency-Based Routing:**
- Route 53 determines user location
- Routes to server with lowest latency
- Different users see different instances based on their location

**Global Application Benefits:**
- Users automatically connect to closest server
- Reduced latency improves user experience
- No manual configuration needed per region

---

## 🎯 Key Takeaways

✅ **Route 53 is managed DNS** – Helps clients find servers through URLs

✅ **Common record types:**
- **A Record** – Maps to IPv4 address
- **AAAA Record** – Maps to IPv6 address
- **CNAME Record** – Maps hostname to hostname
- **Alias Record** – Maps to AWS resources (ELB, CloudFront, S3, RDS)

✅ **DNS flow:** Browser → DNS Query → Route 53 → IP Address → Server

✅ **Four routing policies:**
- **Simple** – No health checks, basic routing
- **Weighted** – Distribute traffic across multiple instances (load balancing)
- **Latency** – Route to closest server (minimize latency)
- **Failover** – Automatic failover for disaster recovery (requires health checks)

✅ **Health checks:** Available for Weighted, Latency, and Failover policies (required for Failover)

✅ **Use cases:**
- **Weighted** – Traffic distribution and load balancing
- **Latency** – Global applications with low latency requirements
- **Failover** – Disaster recovery and high availability

---


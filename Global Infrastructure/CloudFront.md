# ☁️ Amazon CloudFront

## 📋 Overview

**Amazon CloudFront** is a Content Delivery Network (CDN) that improves read performance by caching website content at edge locations worldwide. CloudFront reduces latency and improves user experience by serving content from locations closest to users.

---

## 🔍 What is CloudFront?

**CloudFront** is a global CDN service that:
- **Caches content** at edge locations worldwide
- **Reduces latency** by serving content from locations closest to users
- **Improves performance** for global applications
- **Provides DDoS protection** through distributed infrastructure

---

## 🌐 CloudFront Infrastructure

### 📍 Edge Locations and Points of Presence

- **Hundreds of points of presence** globally
- **Edge locations** and **edge caches** distributed worldwide
- **~216 points of presence** in the AWS global network
- **Content cached** at edge locations for faster delivery

---

## 🎯 Key Benefits

### 1. **Improved Read Performance**
- Content cached at edge locations
- Faster content delivery to users worldwide

### 2. **Reduced Latency**
- Users connect to nearest edge location
- Lower latency compared to origin servers

### 3. **Better User Experience**
- Faster page loads and content delivery
- Consistent performance globally

### 4. **DDoS Protection**
- Distributed infrastructure makes attacks harder
- Protected by AWS Shield and WAF (Web Application Firewall)

---

## 🏗️ How CloudFront Works

### 📊 Request Flow

```
User → Edge Location → Check Cache → (Cache Hit) Serve from Edge
                                    → (Cache Miss) Fetch from Origin → Cache → Serve to User
```

**Step-by-step:**
1. **User requests content** from edge location
2. **Edge location checks cache:**
   - **Cache Hit:** Content served directly from edge (fast)
   - **Cache Miss:** Edge fetches from origin, caches it, then serves to user
3. **Subsequent requests** from same edge location served from cache

### 🌍 Global Distribution Example

**Scenario:** S3 bucket in Australia, users worldwide

- **User in US:** Requests from US edge location → CloudFront fetches from Australia → Caches at US edge → Serves to user
- **Next US user:** Requests from US edge location → Served directly from cache (no Australia fetch)
- **User in China:** Requests from China edge location → CloudFront fetches from Australia → Caches at China edge → Serves to user

**Result:** Content from one region distributed globally through edge locations.

---

## 🎯 CloudFront Origins

Origins are the backends that CloudFront connects to for content.

### 1. **Amazon S3 Bucket**
- **Use case:** Distribute and cache files
- **Feature:** Upload files directly to S3 through CloudFront
- **Security:** Origin Access Control (OAC) secures access between CloudFront and S3
- **Requirement:** S3 bucket policy must be configured

### 2. **VPC Origin**
- **Use case:** Applications hosted in private subnets within VPC
- **Supported resources:**
  - Private Application Load Balancer
  - Private Network Load Balancer
  - Private EC2 instances
- **Benefit:** Access private resources through CloudFront

### 3. **Custom Origin (HTTP)**
- **Use case:** Any public HTTP backend
- **Examples:**
  - S3 static website (must enable static website hosting first)
  - Public load balancer
  - Any public HTTP server
- **Protocol:** HTTP/HTTPS

---

## 🔐 Origin Access Control (OAC)

**OAC** secures access between CloudFront and S3:
- **Purpose:** Control how CloudFront accesses S3 buckets
- **Implementation:** Configure OAC in CloudFront distribution
- **S3 Bucket Policy:** Must be modified to allow CloudFront access
- **Security:** Prevents direct S3 access, forces access through CloudFront

---

## 📊 CloudFront vs S3 Cross-Region Replication

| Aspect | CloudFront (CDN) | S3 Cross-Region Replication |
|--------|------------------|------------------------------|
| **Infrastructure** | Global edge network (~216 PoPs) | Region-specific setup |
| **Caching** | Files cached at edge locations (e.g., 1 day) | No caching, near real-time updates |
| **Scope** | Worldwide distribution | Specific regions only |
| **Use Case** | Static content available globally | Dynamic content in few regions |
| **Read/Write** | Read-optimized | Read-only replication |
| **Purpose** | Cache content globally | Replicate entire bucket to another region |

**Key Difference:**
- **CloudFront:** CDN for caching static content worldwide
- **S3 Cross-Region Replication:** Replication for dynamic content in specific regions

---

## 🧪 Hands-On: CloudFront Distribution with S3 Origin

### 📋 Overview

This hands-on demonstrates how to create a CloudFront distribution with a private S3 bucket as the origin, allowing secure access to S3 objects without making them public.

---

### 📝 Step 1: Create S3 Bucket and Upload Files

1. **Navigate to S3 Console** → **Create bucket**
2. **Bucket name:** `demo-cloudfront-yourname-v4` (globally unique)
3. **Leave defaults** → **Create bucket**
4. **Upload files:**
   - Upload `index.html`, `coffee.jpg`, `beach.jpeg`
   - Files are **private by default** (Access Denied on direct S3 URLs)

> 💡 **Note:** Direct S3 object URLs will show "Access Denied" because objects are private.

---

### 📝 Step 2: Create CloudFront Distribution

1. **Navigate to CloudFront Console** → **Create distribution**
2. **Select plan:**
   - Choose **Free plan** (sufficient for this demo)
   - Includes: Always-on DDoS protection, geographic traffic blocking, global CDN, free TLS certificates
3. **Distribution name:** `demo-new-cloudfront`
4. **Origin type:** Amazon S3
5. **Select S3 bucket:** Browse and select your bucket (`demo-cloudfront-yourname-v4`)
6. **Allow private S3 bucket access:** ✅ Yes
7. **Use recommended origin settings:** ✅ Yes
8. **Use recommended cache settings:** ✅ Yes
9. **Web Application Firewall:** Not needed for this demo
10. **Create distribution**

> ⏱️ **Note:** Distribution creation takes a few minutes to deploy.

---

### 📝 Step 3: Verify S3 Bucket Policy

1. **Go to S3 Console** → Your bucket → **Permissions** → **Bucket policy**
2. **Verify:** CloudFront automatically created a bucket policy allowing access from your distribution
3. **Result:** CloudFront can now access private S3 objects

---

### 📝 Step 4: Test CloudFront Distribution

1. **Get CloudFront domain name:**
   - CloudFront Console → Your distribution → Copy **Distribution domain name**
   - Format: `d1234567890.cloudfront.net`

2. **Test individual files:**
   - `https://your-distribution.cloudfront.net/coffee.jpg` → Image loads
   - `https://your-distribution.cloudfront.net/beach.jpeg` → Image loads
   - `https://your-distribution.cloudfront.net/index.html` → Full page with images loads

3. **Verify access:**
   - All files accessible through CloudFront
   - S3 bucket remains private (direct S3 URLs still show Access Denied)

---

### 📝 Step 5: Observe Caching Behavior

1. **First request:** Load `beach.jpeg` → May take a moment (cache miss, fetching from S3)
2. **Second request:** Reload `beach.jpeg` → **Instant loading** (served from cache)
3. **Result:** Subsequent requests are much faster due to edge caching

---

### 🔍 Key Observations

**Private S3 Access:**
- S3 bucket objects remain private
- CloudFront can access them via bucket policy
- Users access content through CloudFront, not directly from S3

**Automatic Bucket Policy:**
- CloudFront automatically creates bucket policy
- Policy allows CloudFront distribution to access S3 bucket
- No manual policy configuration needed

**Caching Benefits:**
- First request: Fetches from S3 origin (cache miss)
- Subsequent requests: Served from edge cache (cache hit)
- Much faster loading times for cached content

**Security:**
- S3 objects not publicly accessible
- Access only through CloudFront distribution
- Origin Access Control (OAC) secures the connection

---

## 🎯 Key Takeaways

✅ **CloudFront is a CDN** – Content Delivery Network for caching content globally

✅ **Benefits:**
- Improved read performance
- Reduced latency
- Better user experience
- DDoS protection

✅ **Infrastructure:**
- Hundreds of edge locations and points of presence
- ~216 points of presence globally
- Content cached at edge locations

✅ **How it works:**
- User requests from edge location
- Edge checks cache (hit = serve, miss = fetch from origin)
- Content cached for subsequent requests

✅ **Three origin types:**
- **S3 Bucket** – File distribution (secured with OAC)
- **VPC Origin** – Private resources (ALB, NLB, EC2)
- **Custom Origin** – Public HTTP backends

✅ **Origin Access Control (OAC)** – Secures CloudFront access to S3 buckets

✅ **CloudFront vs S3 Replication:**
- **CloudFront:** Global caching for static content
- **S3 Replication:** Region-specific replication for dynamic content

---


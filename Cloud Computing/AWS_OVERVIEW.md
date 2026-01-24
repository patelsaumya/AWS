# 🚀 AWS Overview

## 📜 History of AWS

* **2002** – AWS launched internally at Amazon.
* **2004** – First public service released: **Amazon SQS**.
* **2006** – Relaunch with **SQS, S3, and EC2**.
* Expanded globally beyond the US → Europe, Asia, etc.
* Today, AWS powers companies like **Netflix, Dropbox, Airbnb, NASA, McDonald's, Fox, Activision**.

---

## 📊 AWS Market Position

* **Leader in Gartner Magic Quadrant** (13+ years in a row).
* **Revenue**: ~$90B (2023).
* **Market share (Q1 2024)**: ~31%.
* **2nd place**: Microsoft Azure (~25%).
* **1M+ active users**.
* AWS is the **pioneer & leader** in cloud computing.

---

## 🌍 What Can You Build on AWS?

* **Enterprise IT migration**.
* **Backup & storage** solutions.
* **Big Data & Analytics**.
* **Websites & mobile backends**.
* **Gaming infrastructure**.
* **Machine Learning / AI apps**.
* **Global-scale applications** across industries.

---

## 🌐 AWS Global Infrastructure

### 1. **Regions**

* AWS Regions = **clusters of data centers** around the world.
* Examples: `us-east-1` (N. Virginia), `eu-west-3` (Paris), `ap-south-1` (Mumbai).
* Services are often **region-specific**.
* **Choosing a region depends on**:

  * **Compliance** → some countries require data residency.
  * **Latency** → deploy close to your users.
  * **Service availability** → not all services exist in every region.
  * **Pricing** → cost varies across regions.

---

### 2. **Availability Zones (AZs)**

* Each **Region = 3 to 6 Availability Zones** (usually 3).
* Example: Sydney → `ap-southeast-2a`, `ap-southeast-2b`, `ap-southeast-2c`.
* Each AZ = **1+ discrete data centers** with redundant networking & power.
* AZs are **isolated from disasters** but connected with **low-latency, high-bandwidth links**.
* Together, they form a **fault-tolerant region**.

---

### 3. **Points of Presence (Edge Locations)**

* **400+ Points of Presence (PoPs)** across **90 cities, 40 countries**.
* Used to **cache & deliver content** with low latency.
* Support services like **CloudFront (CDN)**, Route 53, and WAF.

---

## 🌎 Global vs Regional Services

AWS services can be either **Region-Scoped** or **Global-Scoped**:

### 🔹 Region-Scoped Services

* Operate **within a single AWS Region**.
* Resources, data, and workloads are tied to the chosen region.
* ✅ Best for **compliance, low latency, and regional deployment**.

**Examples:**

* EC2 (servers)
* RDS (databases)
* Lambda (serverless functions)
* Elastic Beanstalk

### 🔹 Global-Scoped Services

* Operate **across all AWS Regions**.
* Centralized management and worldwide operation.
* ✅ Best for **identity, traffic routing, and edge delivery**.

**Examples:**

* IAM (account-wide identity & access)
* Route 53 (DNS)
* CloudFront (CDN)
* WAF / Shield (security)

## 🔑 Summary Table

| Scope             | Where It Operates              | Examples                            | Use Case                                                                   |
| ----------------- | ------------------------------ | ----------------------------------- | -------------------------------------------------------------------------- |
| **Region-Scoped** | Only inside **one AWS Region** | EC2, RDS, Lambda, S3 (region-based) | For **low latency**, **local compliance**, **regional apps**               |
| **Global-Scoped** | Works **across all Regions**   | IAM, Route 53, CloudFront, WAF      | For **centralized control**, **global scale**, **security & traffic mgmt** |

👉 **Rule of Thumb**: Infra & compute = **Region-Scoped**, while identity, DNS, and CDN = **Global-Scoped**.

---

## 🏷️ Amazon Resource Names (ARNs)

**ARNs (Amazon Resource Names)** uniquely identify AWS resources across the entire AWS platform.

* **Format**: `arn:partition:service:region:account-id:resource-type/resource-id`
* **Example**: `arn:aws:ec2:us-east-1:123456789012:instance/i-1234567890abcdef0`
* **Global uniqueness** → Every AWS resource has a unique ARN
* **Used for**: IAM policies, resource references, cross-service communication

---

## ⛑️ Shared Responsibility Model

- **Customer** : Security *in* the cloud
- **AWS** : Security *of* the cloud

---

## ✅ Key Takeaways

* AWS started as Amazon’s internal infra → became **world’s #1 cloud provider**.
* Provides **flexibility, scalability, global reach** for all industries.
* Built on **Regions + AZs + Edge Locations** for **performance, fault tolerance, and low latency**.
* Services are either **Global** or **Region-specific**, depending on their scope.
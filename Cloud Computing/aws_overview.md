# 🚀 AWS Overview

## 📜 History of AWS
- **2002** – AWS launched internally at Amazon.
- **2004** – First public service released: **Amazon SQS**.
- **2006** – Relaunch with **SQS, S3, and EC2**.
- Expanded globally beyond the US → Europe, Asia, etc.
- Today, AWS powers companies like **Netflix, Dropbox, Airbnb, NASA, McDonald's, Fox, Activision**.

---

## 📊 AWS Market Position
- **Leader in Gartner Magic Quadrant** (13+ years in a row).
- **Revenue**: ~$90B (2023).
- **Market share (Q1 2024)**: ~31%.
- **2nd place**: Microsoft Azure (~25%).
- **1M+ active users**.
- AWS is the **pioneer & leader** in cloud computing.

---

## 🌍 What Can You Build on AWS?
- **Enterprise IT migration**.
- **Backup & storage** solutions.
- **Big Data & Analytics**.
- **Websites & mobile backends**.
- **Gaming infrastructure**.
- **Machine Learning / AI apps**.
- **Global-scale applications** across industries.

---

## 🌐 AWS Global Infrastructure

### 1. **Regions**
- AWS Regions = **clusters of data centers** around the world.
- Examples: `us-east-1` (N. Virginia), `eu-west-3` (Paris), `ap-south-1` (Mumbai).
- Services are often **region-specific**.
- **Choosing a region depends on**:
    - **Compliance** → some countries require data residency.
    - **Latency** → deploy close to your users.
    - **Service availability** → not all services exist in every region.
    - **Pricing** → cost varies across regions.

---

### 2. **Availability Zones (AZs)**
- Each **Region = 3 to 6 Availability Zones** (usually 3).
- Example: Sydney → `ap-southeast-2a`, `ap-southeast-2b`, `ap-southeast-2c`.
- Each AZ = **1+ discrete data centers** with redundant networking & power.
- AZs are **isolated from disasters** but connected with **low-latency, high-bandwidth links**.
- Together, they form a **fault-tolerant region**.

---

### 3. **Points of Presence (Edge Locations)**
- **400+ Points of Presence (PoPs)** across **90 cities, 40 countries**.
- Used to **cache & deliver content** with low latency.
- Support services like **CloudFront (CDN)**, Route 53, and WAF.

---

## 🌎 Global vs Regional Services
- **Global Services** (not tied to a single region):
    - IAM
    - Route 53
    - CloudFront
    - WAF

- **Regional Services** (region-scoped):
    - EC2
    - Elastic Beanstalk
    - Lambda
    - Rekognition

👉 To check service availability → Use the [AWS Region Table](https://aws.amazon.com/about-aws/global-infrastructure/regional-product-services/).

---

## ✅ Key Takeaways
- AWS started as Amazon’s internal infra → became **world’s #1 cloud provider**.
- Provides **flexibility, scalability, global reach** for all industries.
- Built on **Regions + AZs + Edge Locations** for **performance, fault tolerance, and low latency**.
- Services are either **Global** or **Region-specific**.
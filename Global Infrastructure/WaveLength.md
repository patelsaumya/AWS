# 📡 AWS Wavelength

## 📋 Overview

**AWS Wavelength** deploys AWS infrastructure and services directly into telecommunications providers' datacenters at the edge of 5G networks, enabling ultra-low latency applications for mobile users.

---

## 🔍 What is AWS Wavelength?

**AWS Wavelength Zones** are:
- **Infrastructure deployments** embedded in telecom providers' datacenters
- **At the edge of 5G networks** (within the 5G network itself)
- **AWS services available** – EC2, EBS, VPC can be deployed to Wavelength Zones
- **Ultra-low latency** for 5G mobile device users

**Key Concept:** Deploy AWS compute and storage directly at the 5G network edge.

---

## 🏗️ How Wavelength Works

```
5G Mobile User → 5G Network → Wavelength Zone (EC2/EBS/VPC)
                                    ↓
                            Parent AWS Region (RDS, DynamoDB)
```

**Architecture:**
1. **Wavelength Zone** deployed in telecom carrier's 5G network datacenter
2. **Carrier Gateway** provides connectivity between Wavelength Zone and the carrier network (and devices on the carrier network)
3. **EC2 instances, EBS volumes, VPC** deployed directly in Wavelength Zone
4. **5G mobile users** access applications with ultra-low latency through carrier network
5. **Parent AWS Region** connection available for accessing RDS, DynamoDB, etc.

**Traffic Flow:**
- **Traffic stays within CSP network** – Never reaches AWS (unless needed)
- **Secure connection to AWS** available when required (e.g., accessing databases)
- **Connected to parent region** for accessing AWS services like RDS, DynamoDB

---

## ✅ Key Features

- **Ultra-low latency** – Applications deployed at 5G network edge
- **No additional charges** – No extra service agreements for using Wavelength
- **AWS services at edge** – EC2, EBS, VPC available in Wavelength Zones
- **Parent region access** – Secure connection to AWS region for additional services

---

## 🎯 Use Cases

**Ultra-low latency applications enabled by 5G:**

- **Smart Cities** – Real-time city infrastructure management
- **ML-Assisted Diagnostics** – Medical diagnostics with low latency
- **Connected Vehicles** – Real-time vehicle communication
- **Interactive Live Video Streams** – Low-latency video streaming
- **AR and VR** – Augmented and Virtual Reality applications
- **Real-time Gaming** – Mobile gaming with minimal latency

**Common Theme:** Applications requiring **ultra-low latency** and **edge deployment** for 5G mobile users.

---

## 🎯 Key Takeaways

✅ **Wavelength = AWS at 5G network edge** – Infrastructure in telecom datacenters

✅ **Ultra-low latency** – Applications deployed directly in 5G network edge

✅ **Available services:** EC2, EBS, VPC in Wavelength Zones

✅ **Traffic stays in CSP network** – Doesn't reach AWS unless needed for database access

✅ **Connected to parent region** – Can access RDS, DynamoDB in main AWS region

✅ **Use cases:** Smart Cities, Connected Vehicles, AR/VR, Real-time Gaming, Live Video

✅ **No additional charges** – Standard AWS pricing applies

---


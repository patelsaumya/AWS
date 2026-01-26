# 🔑 AWS SSM Parameter Store Overview

## 📋 Overview

**AWS SSM Parameter Store** is a serverless service that allows you to store configuration data and secrets securely on AWS. You can store API keys, passwords, configurations, and other sensitive data in a centralized location with version tracking and optional encryption.

---

## 🔍 What is SSM Parameter Store?

**SSM Parameter Store** is a secure, scalable, and durable storage service for application configuration and secrets. It provides a centralized place to manage configurations for many applications, with IAM-based access control, version tracking, and optional encryption using KMS.

### 🔑 Key Characteristics

- **Serverless** – No infrastructure to provision or manage
- **Scalable** – Handles many API calls simultaneously
- **Durable** – Highly available and reliable
- **Secure** – Access controlled via IAM, optional encryption with KMS
- **Version tracking** – Track parameter changes over time
- **Easy to use** – Simple interface for storing and retrieving values

---

## 💾 What Can You Store?

- **API keys** – Store API credentials securely
- **Passwords** – Encrypted password storage
- **Configurations** – Application configuration values
- **Database connection strings** – Store database credentials
- **Any string values** – Store any configuration data

---

## 🏗️ Parameter Types

### 1. **String**
- Plain text configuration values
- Example: Application settings, URLs

### 2. **StringList**
- List of values (comma-separated)
- Example: Multiple IP addresses, list of regions

### 3. **SecureString**
- Encrypted values using KMS
- Use for sensitive data: API keys, passwords, secrets
- Automatically encrypted at rest

---

## 📊 Parameter Tiers

### **Standard** (Free Tier)
- Up to 4 KB parameter value size
- No parameter policies
- Standard throughput

### **Advanced** (Paid)
- Up to 8 KB parameter value size
- Parameter policies (expiration, notifications)
- Higher throughput limits

---

## 🔐 Security Features

- **IAM access control** – Control access to each parameter using IAM policies
- **KMS encryption** – SecureString parameters encrypted with AWS KMS
- **Version tracking** – Track parameter changes over time
- **Audit trail** – Monitor parameter access and changes

---

## 🛠️ How to Use Parameter Store

1. **Create Parameter:**
   - Navigate to Systems Manager → Parameter Store
   - Click "Create parameter"
   - Enter parameter name
   - Choose tier (Standard or Advanced)
   - Select type (String, StringList, or SecureString)
   - Enter value
   - Create parameter

2. **Retrieve Parameter:**
   - View parameter in Parameter Store
   - Click on parameter to see value
   - Use AWS SDK/CLI to retrieve programmatically

3. **Edit Parameter:**
   - Edit parameter value
   - Version tracking automatically creates new versions
   - View version history

4. **Delete Parameter:**
   - Delete when no longer needed

---

## 📊 Summary

| Aspect | Description |
|--------|-------------|
| **Type** | Serverless configuration and secrets storage |
| **Storage** | API keys, passwords, configurations |
| **Tiers** | Standard (free) and Advanced (paid) |
| **Parameter Types** | String, StringList, SecureString |
| **Encryption** | SecureString encrypted with KMS |
| **Security** | IAM-based access control |
| **Versioning** | Automatic version tracking |

---

## 🎯 Key Takeaways

✅ **SSM Parameter Store stores configuration and secrets** – API keys, passwords, configurations

✅ **Serverless, scalable, durable** – No infrastructure to manage, handles high throughput

✅ **Secure** – IAM access control, optional KMS encryption for SecureString

✅ **Version tracking** – Track parameter changes over time

✅ **Parameter types:**
- **String** – Plain text values
- **StringList** – Comma-separated lists
- **SecureString** – Encrypted values (KMS)

✅ **Two tiers:**
- **Standard** (free) – Up to 4 KB, standard throughput
- **Advanced** (paid) – Up to 8 KB, parameter policies, higher throughput

✅ **Centralized storage** – Manage configurations for many applications in one place

---


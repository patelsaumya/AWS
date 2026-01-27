# 🔒 Amazon S3 Security

## 📋 Overview

Amazon S3 provides multiple layers of security to protect your data. Understanding S3 security is crucial for properly configuring access controls, preventing data leaks, and ensuring only authorized users can access your objects. S3 security operates through both user-based and resource-based controls.

---

## 🔐 Types of S3 Security

### 👤 User-Based Security

**IAM Policies** control what actions specific IAM users can perform on S3 resources.

#### 🔑 Key Characteristics

- **Applied to:** IAM users, groups, or roles
- **Controls:** Which API calls are allowed for specific IAM principals
- **Scope:** User-centric permissions
- **Management:** Through IAM service

#### 📝 Example Use Cases

- Allow specific users to read objects from certain buckets
- Grant developers access to upload files to staging buckets
- Restrict delete permissions to admin users only

### 🪣 Resource-Based Security

**Resource-based security** is applied directly to S3 resources (buckets and objects).

#### 📊 S3 Bucket Policies

- **Scope:** Bucket-wide rules
- **Management:** Directly from S3 console
- **Format:** JSON-based policies
- **Use cases:** Public access, cross-account access, conditional access

#### 📝 Object Access Control Lists (ACLs)

- **Scope:** Individual object level
- **Granularity:** Fine-grained permissions
- **Status:** Can be disabled (recommended for most use cases)
- **Legacy:** Less commonly used in modern implementations

#### 📝 Bucket Access Control Lists (ACLs)

- **Scope:** Bucket level
- **Usage:** Less common than bucket policies
- **Status:** Can be disabled
- **Recommendation:** Use bucket policies instead

> 💡 **Best Practice:** The most common and recommended way to manage S3 security is through **S3 Bucket Policies**.

---

## ✅ Access Decision Logic

An IAM principal can access an S3 object if **ALL** of the following conditions are met:

### 🔍 Access Evaluation Process

1. **IAM permissions allow it** OR **Resource policy allows it**
2. **AND** there is **no explicit DENY** in any policy

#### 📊 Decision Matrix

| IAM Policy | Resource Policy | Explicit Deny | Result |
|------------|-----------------|---------------|---------|
| ✅ Allow | ❌ Deny | ❌ No | ✅ **Access Granted** |
| ❌ Deny | ✅ Allow | ❌ No | ✅ **Access Granted** |
| ✅ Allow | ✅ Allow | ❌ No | ✅ **Access Granted** |
| ❌ Deny | ❌ Deny | ❌ No | ❌ **Access Denied** |
| ✅ Allow | ✅ Allow | ✅ Yes | ❌ **Access Denied** |

> ⚠️ **Important:** An explicit DENY in any policy always overrides any ALLOW statements.

---

## 🔐 Encryption

Another layer of S3 security involves **encrypting objects** using encryption keys.

### 🔑 Encryption Options

- **Server-Side Encryption (SSE)** – AWS encrypts objects at rest
- **Client-Side Encryption** – You encrypt objects before uploading
- **Encryption in Transit** – HTTPS for data transfer security

---

## 📄 S3 Bucket Policy Structure

### 🔍 JSON-Based Policies

S3 Bucket Policies are **JSON documents** that define permissions for bucket access.

#### 📝 Basic Structure Example

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "PublicReadGetObject",
      "Effect": "Allow",
      "Principal": "*",
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::example-bucket/*"
    }
  ]
}
```

#### 🔍 Policy Components

**1. Resource Block**
- **Purpose:** Defines which buckets and objects the policy applies to
- **Example:** `"arn:aws:s3:::example-bucket/*"`
- **Meaning:** All objects (`*`) within the `example-bucket`

**2. Effect**
- **Options:** `Allow` or `Deny`
- **Purpose:** Whether to permit or prohibit the specified actions

**3. Action**
- **Purpose:** Specifies which S3 API calls are affected
- **Example:** `s3:GetObject` (retrieve objects)
- **Multiple actions:** Can specify multiple API calls

**4. Principal**
- **Purpose:** Defines who the policy applies to
- **Examples:** 
  - `"*"` = Anyone (public access)
  - `"arn:aws:iam::123456789012:user/username"` = Specific user
  - `"arn:aws:iam::123456789012:root"` = Entire account

### 🌐 Example: Public Read Access Policy

The example above creates a policy that:
- **Allows** anyone (`Principal: "*"`)
- **To perform** `GetObject` actions (`Action: "s3:GetObject"`)
- **On all objects** in the example-bucket (`Resource: "...example-bucket/*"`)
- **Result:** Public read access to all objects in the bucket

---

## 🛠️ AWS Policy Generator Tool

### 📋 Overview

AWS provides a web-based **Policy Generator** tool that helps you create IAM policies and S3 bucket policies without manually writing JSON. This tool is particularly useful for beginners or when you need to quickly generate policies for common use cases.

### 🔗 Access the Tool

**AWS Policy Generator:** [https://awspolicygen.s3.amazonaws.com/policygen.html](https://awspolicygen.s3.amazonaws.com/policygen.html)
---

## 🎯 Common S3 Bucket Policy Use Cases

### 1️⃣ Grant Public Access to Bucket

**Use case:** Make a bucket publicly readable (e.g., static website hosting)

**Implementation:**
- Create bucket policy with `Principal: "*"`
- Allow `s3:GetObject` action
- Apply to all objects in bucket

### 2️⃣ Force Object Encryption at Upload

**Use case:** Require all uploaded objects to be encrypted

**Implementation:**
- Create bucket policy with condition requiring encryption headers
- Deny uploads without proper encryption parameters

### 3️⃣ Grant Cross-Account Access

**Use case:** Allow users from another AWS account to access your bucket

**Implementation:**
- Create bucket policy specifying the external account/user as principal
- Define specific permissions for cross-account access

---

## 🌐 Access Scenarios

### 📊 Scenario 1: Public Website Access

```
Internet User → S3 Bucket (with Public Bucket Policy) → Objects
```

**Setup:**
- **User:** Website visitor from worldwide web
- **Goal:** Access files in S3 bucket
- **Solution:** Attach S3 bucket policy allowing public access
- **Result:** Anyone can access objects in the bucket

### 👤 Scenario 2: IAM User Access

```
IAM User → IAM Policy → S3 Bucket → Objects
```

**Setup:**
- **User:** IAM user within your AWS account
- **Goal:** Access S3 bucket from within account
- **Solution:** Assign IAM permissions through user/group policy
- **Result:** User can access S3 bucket based on IAM permissions

### 🖥️ Scenario 3: EC2 Instance Access

```
EC2 Instance → IAM Role → S3 Bucket → Objects
```

**Setup:**
- **User:** EC2 instance needs S3 access
- **Goal:** Allow EC2 to read/write to S3
- **Solution:** Create EC2 instance role with S3 permissions
- **Result:** EC2 instance can access S3 through role credentials

> ⚠️ **Important:** Never use IAM users for EC2 instances. Always use IAM roles.

### 🔄 Scenario 4: Cross-Account Access

```
External AWS Account → IAM User → S3 Bucket Policy → S3 Bucket → Objects
```

**Setup:**
- **User:** IAM user from different AWS account
- **Goal:** Access your S3 bucket from external account
- **Solution:** Create S3 bucket policy allowing cross-account access
- **Result:** External user can access your bucket with defined permissions

---

## 🚫 Block Public Access Settings

### 🔒 Extra Security Layer

**Block Public Access** settings provide an additional security layer to prevent accidental data leaks.

#### 🔍 How It Works

- **Created by AWS** as extra protection against company data leaks
- **Overrides bucket policies** that would make buckets public
- **Prevents public access** even if bucket policy allows it
- **Safety net** against misconfigured bucket policies

#### 📊 Setting Levels

**Bucket Level:**
- Applied to individual buckets
- Set during bucket creation or modified later
- Prevents that specific bucket from becoming public

**Account Level:**
- Applied across all buckets in your AWS account
- Ensures no buckets in your account can ever be public
- Useful for organizations with strict security requirements

#### 🎯 Use Cases

**Leave Enabled When:**
- Bucket should never be public
- Company policy prohibits public buckets
- Storing sensitive or confidential data
- Want protection against misconfigurations

**Disable When:**
- Need to host public websites
- Serving public content (images, videos, documents)
- Creating public APIs or content delivery

> 💡 **Best Practice:** Keep Block Public Access enabled unless you specifically need public buckets. It's easier to disable when needed than to recover from a data leak.

---

## 📊 Summary

| Security Method | Level | Use Case | Management |
|----------------|-------|----------|------------|
| **IAM Policies** | User-based | Control what users can do | IAM Console |
| **Bucket Policies** | Resource-based | Control bucket access, cross-account, public access | S3 Console |
| **Object ACLs** | Object-based | Fine-grained object permissions (legacy) | S3 Console |
| **Bucket ACLs** | Bucket-based | Bucket permissions (legacy) | S3 Console |
| **Block Public Access** | Account/Bucket | Prevent public access even with policies | S3 Console |
| **Encryption** | Object-based | Protect data at rest and in transit | S3 Console |

---

## 🎯 Key Takeaways

- **Multiple security layers** – S3 uses both user-based (IAM) and resource-based (bucket policies) security
- **Bucket policies are preferred** – Most common method for S3 security configuration
- **Access decision logic** – Access granted if IAM OR resource policy allows, AND no explicit deny exists
- **JSON-based policies** – Bucket policies use JSON format with Resource, Effect, Action, and Principal components
- **Flexible use cases** – Support public access, cross-account access, and conditional access
- **Block Public Access** – Safety net that prevents public access even with permissive policies
- **Account-level protection** – Can prevent all buckets in account from becoming public
- **Encryption available** – Additional layer of security for data protection
- **Explicit deny wins** – Any explicit DENY statement overrides all ALLOW statements

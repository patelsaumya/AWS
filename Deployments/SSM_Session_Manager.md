# 🔐 AWS SSM Session Manager Overview

## 📋 Overview

**AWS SSM Session Manager** is a feature of Systems Manager that allows you to start a secure shell session on EC2 instances and on-premises servers **without SSH access**, bastion hosts, or SSH keys. This means port 22 can remain closed, providing better security.

---

## 🔍 What is SSM Session Manager?

**SSM Session Manager** enables secure shell access to EC2 instances and on-premises servers through the SSM service. The EC2 instance's SSM Agent connects to the Session Manager service, allowing users to access instances and execute commands without traditional SSH.

### 🔑 Key Characteristics

- **No SSH required** – No need for SSH keys or port 22 access
- **No bastion host** – Direct access through SSM service
- **Enhanced security** – Port 22 can remain closed
- **Multi-platform** – Supports Linux, macOS, and Windows
- **Audit logging** – Session history and logs saved to S3 or CloudWatch Logs

---

## 🏗️ How SSM Session Manager Works

1. **SSM Agent** – EC2 instance has SSM Agent installed (pre-installed on Amazon Linux 2)
2. **IAM Role** – EC2 instance must have IAM instance profile with **AmazonSSMManagedInstanceCore** policy
3. **Connection** – SSM Agent connects to Session Manager service
4. **Access** – Users access instances through Session Manager service (no direct SSH)

### 📊 Architecture

```
User → Session Manager Service → SSM Agent → EC2 Instance
(No port 22 needed, no SSH keys)
```

---

## 🔐 Security Benefits

- **Port 22 closed** – No need to open SSH port in security groups
- **No SSH keys** – Eliminates key management overhead
- **No bastion host** – Direct access through AWS service
- **Audit trail** – All sessions logged to S3 or CloudWatch Logs
- **Centralized access** – Access controlled through IAM

---

## 🆚 EC2 Access Methods Comparison

| Method | SSH Keys | Port 22 | Bastion Host | Security |
|--------|----------|---------|--------------|---------|
| **SSH** | ✅ Required | ✅ Must be open | Optional | Standard |
| **EC2 Instance Connect** | ❌ Not needed | ✅ Must be open | ❌ Not needed | Better |
| **SSM Session Manager** | ❌ Not needed | ❌ Can be closed | ❌ Not needed | **Best** |

---

## 📋 Requirements

### For EC2 Instances

1. **SSM Agent** – Must be installed (pre-installed on Amazon Linux 2 and some Ubuntu AMIs)
2. **IAM Instance Profile** – Attach IAM role with **AmazonSSMManagedInstanceCore** managed policy
3. **Fleet Manager** – Instance appears as "managed node" when SSM Agent is online

### IAM Role Setup

- **Service:** Amazon EC2
- **Policy:** `AmazonSSMManagedInstanceCore`
- **Purpose:** Allows EC2 instance to communicate with SSM service

---

## 🛠️ Using Session Manager

1. **Navigate to Systems Manager** → **Fleet Manager**
2. **Verify managed nodes** – EC2 instances with SSM Agent online appear here
3. **Start Session** – Go to **Session Manager** → **Start session**
4. **Select instance** – Choose the EC2 instance
5. **Execute commands** – Secure shell session opens (no SSH needed)

---

## 📊 Logging and Audit

- **Session history** – All sessions are logged
- **Log destinations** – Send logs to Amazon S3 or CloudWatch Logs
- **Audit trail** – Track who accessed which instances and when

---

## 📊 Summary

| Aspect | Description |
|--------|-------------|
| **Type** | Secure shell access feature of SSM |
| **Access Method** | Through SSM service (no SSH) |
| **Port 22** | Not required (can be closed) |
| **SSH Keys** | Not required |
| **Platform Support** | Linux, macOS, Windows |
| **Logging** | S3 or CloudWatch Logs |
| **Requirement** | IAM role with AmazonSSMManagedInstanceCore policy |

---

## 🎯 Key Takeaways

✅ **SSM Session Manager provides secure shell access** without SSH, SSH keys, or port 22

✅ **Enhanced security** – Port 22 can remain closed, no bastion host needed

✅ **IAM role required** – EC2 instance needs IAM instance profile with `AmazonSSMManagedInstanceCore` policy

✅ **SSM Agent required** – Must be installed on instances (pre-installed on Amazon Linux 2)

✅ **Fleet Manager** – View all managed nodes (instances with SSM Agent online)

✅ **Audit logging** – Session history saved to S3 or CloudWatch Logs

✅ **Three ways to access EC2:**
1. SSH (port 22 + SSH keys)
2. EC2 Instance Connect (port 22, no keys)
3. **SSM Session Manager** (no port 22, no keys) ⭐ **Most secure**

---


# 🧩 AWS IAM Roles

## 📘 Overview

In AWS Identity and Access Management (IAM), **Roles** are a special kind of identity that allows AWS services to perform actions **on your behalf**.  
Unlike IAM users, **roles are not associated with a specific person** — they are meant to be **assumed** by AWS services or other entities that need permissions to interact with your AWS resources.

---

## 🔑 What Is an IAM Role?

An **IAM Role** defines a **set of permissions** that determine what actions are allowed or denied within your AWS account.  
However, roles do **not have long-term credentials** (like usernames or passwords). Instead, they use **temporary security credentials** provided when the role is assumed.

### 💡 Key Idea
> IAM Roles allow AWS services or external users to access resources **securely and temporarily** without needing permanent access keys.

---

## ⚙️ How IAM Roles Work

When an AWS service (like an EC2 instance or Lambda function) needs to perform actions in your account — such as reading from S3 or writing to DynamoDB — it must be **granted permission**.

To achieve this, we **attach an IAM Role** to that service.

### 🔄 Example Workflow

1. You create an **IAM Role** and attach a **policy** that defines its permissions.
2. You assign that role to an AWS service (e.g., EC2, Lambda).
3. When the service performs an API call, AWS automatically provides it with **temporary credentials** tied to that role.
4. These credentials are used to make authorized API requests.

---

## 💻 Example: EC2 Instance Role

Let’s say you have an EC2 instance that needs to **read files from an S3 bucket**.

Instead of storing AWS access keys on the instance (which is insecure), you:
1. Create an **IAM Role** with a policy allowing `s3:GetObject` access.
2. Attach that role to your EC2 instance.
3. When your instance runs an application that calls S3 APIs, AWS uses the **role’s temporary credentials** to authenticate automatically.

✅ **Result:** The EC2 instance can securely access S3 without embedding any credentials.

---

## 🧠 Common Types of IAM Roles

| AWS Service | Role Purpose |
|--------------|---------------|
| **EC2 Instance Role** | Allows EC2 instances to access other AWS services (like S3, CloudWatch). |
| **Lambda Execution Role** | Grants AWS Lambda functions permission to access other services. |
| **CloudFormation Role** | Lets AWS CloudFormation manage resources on your behalf. |
| **ECS Task Role** | Provides ECS containers with permissions to call AWS APIs. |
| **Cross-Account Role** | Allows access between different AWS accounts. |

---

## 🧱 Components of an IAM Role

| Component | Description |
|------------|-------------|
| **Trust Policy** | Defines who (which entities or services) can assume the role. |
| **Permissions Policy** | Defines what actions and resources the role can access. |
| **Temporary Credentials** | Generated automatically when the role is assumed. |

---

## 🚨 Security Best Practices

- **Never use IAM users for AWS services.** Use **roles** instead.
- **Grant least privilege** — only the permissions needed for a task.
- **Regularly review** which services and users can assume each role.
- **Use CloudTrail** to monitor role assumption and activity.

---

## 🚀 Summary

| Feature | Description |
|----------|-------------|
| **Purpose** | Grant permissions to AWS services or external entities. |
| **Used By** | Services like EC2, Lambda, CloudFormation, or cross-account users. |
| **Credentials** | Temporary (auto-rotated by AWS). |
| **Policies** | Trust Policy (who can assume) + Permissions Policy (what can be done). |
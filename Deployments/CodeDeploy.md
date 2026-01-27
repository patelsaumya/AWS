# 🚀 AWS CodeDeploy Overview

## 📋 Overview

**AWS CodeDeploy** is a deployment service that automates application deployments to EC2 instances and on-premises servers. Unlike Beanstalk or CloudFormation, CodeDeploy is completely independent and focuses solely on deploying application code from one version to another (e.g., V1 to V2).

---

## 🔍 What is CodeDeploy?

**AWS CodeDeploy** is a hybrid deployment service that automates application deployments across EC2 instances and on-premises servers. You provision and configure servers ahead of time, and CodeDeploy handles the deployment process through a single interface.

### 🔑 Key Characteristics

- **Independent service** – Works independently of Beanstalk or CloudFormation
- **Hybrid service** – Supports both EC2 instances and on-premises servers
- **Automatic deployments** – Upgrades applications from one version to another automatically
- **Single interface** – Deploy to both EC2 and on-premises from one place
- **Server provisioning** – You must provision servers ahead of time
- **CodeDeploy agent** – Must be installed on servers to enable deployments

---

## 🏗️ How CodeDeploy Works

1. **Provision servers** – Set up EC2 instances or on-premises servers
2. **Install CodeDeploy agent** – Configure servers with CodeDeploy agent
3. **Deploy application** – CodeDeploy automatically upgrades applications from V1 to V2
4. **Manage deployments** – Use single interface for both EC2 and on-premises servers

---

## 💡 Use Cases

- **Application version upgrades** – Deploy new application versions automatically
- **Hybrid deployments** – Deploy to both AWS EC2 and on-premises servers
- **On-premises to AWS migration** – Use same deployment process for both environments
- **Multi-server deployments** – Deploy to many EC2 instances simultaneously

---

## 🆚 CodeDeploy vs Other Services

| Aspect | CodeDeploy | Beanstalk | CloudFormation |
|--------|------------|-----------|----------------|
| **Focus** | Application deployment | Full PaaS platform | Infrastructure as Code |
| **Scope** | Code deployment only | Application + infrastructure | Infrastructure only |
| **On-Premises** | ✅ Supported | ❌ AWS only | ❌ AWS only |
| **Independence** | ✅ Independent | ❌ AWS managed | ❌ AWS only |

---

## 📊 Summary

| Aspect | Description |
|--------|-------------|
| **Type** | Hybrid deployment service |
| **Targets** | EC2 instances and on-premises servers |
| **Independence** | Works independently of other AWS services |
| **Agent Required** | CodeDeploy agent must be installed on servers |
| **Key Benefit** | Single interface for deploying to EC2 and on-premises |

---

## 🎯 Key Takeaways

✅ **CodeDeploy is independent** – Doesn't require Beanstalk or CloudFormation

✅ **Hybrid service** – Works with both EC2 instances and on-premises servers

✅ **Automatic deployments** – Upgrades applications from version to version automatically

✅ **Server provisioning required** – You must provision and configure servers ahead of time

✅ **CodeDeploy agent** – Must be installed on all target servers (EC2 and on-premises)

✅ **Single interface** – Deploy to both EC2 and on-premises servers from one place

✅ **Migration tool** – Useful for transitioning from on-premises to AWS using the same deployment process

---


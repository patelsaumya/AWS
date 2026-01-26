# ⚙️ AWS Systems Manager (SSM) Overview

## 📋 Overview

**AWS Systems Manager (SSM)** is a hybrid service that helps you manage your fleet of EC2 instances and on-premises systems at scale. It provides operational insights about your infrastructure and offers a suite of 10+ products for managing, patching, and configuring servers across both AWS and on-premises environments.

---

## 🔍 What is SSM?

**AWS Systems Manager** is a management service that provides operational insights and a comprehensive suite of tools to manage EC2 instances and on-premises systems. It's a hybrid service because it works with both AWS resources and on-premises infrastructure.

### 🔑 Key Characteristics

- **Hybrid service** – Works with both EC2 instances and on-premises systems
- **Fleet management** – Manage servers at scale
- **Operational insights** – Get visibility into infrastructure state
- **Suite of products** – 10+ integrated management tools
- **Multi-platform** – Works with Linux, Windows, Mac OS, and Raspberry Pi

---

## 🛠️ Key Features

### 🔧 Most Important Features

- **Automated patching** – Patch all servers and instances for enhanced compliance
- **Run commands** – Execute commands across entire fleet of servers directly from SSM
- **SSM Parameter Store** – Store and manage configuration data securely
- **Operational insights** – Monitor and understand infrastructure state

---

## 🏗️ How SSM Works

1. **Install SSM Agent** – Install the SSM agent on all systems you want to manage
   - **Default installation:** Amazon Linux AMI and some Ubuntu AMIs have SSM agent pre-installed
   - **On-premises:** Must install SSM agent on virtual machines
   - **EC2 instances:** Install SSM agent if not pre-installed

2. **Agent Reporting** – SSM agent runs in background and reports back to SSM service in AWS

3. **Management** – Once agent is installed, use SSM service to:
   - Run commands across all servers
   - Patch servers automatically
   - Configure servers consistently

### ⚠️ Troubleshooting

If an instance cannot be controlled by SSM, it's likely an **SSM agent issue** (not installed, not running, or misconfigured).

---

## 📊 Summary

| Aspect | Description |
|--------|-------------|
| **Type** | Hybrid management service |
| **Targets** | EC2 instances and on-premises systems |
| **Key Features** | Automated patching, run commands, Parameter Store, operational insights |
| **Platform Support** | Linux, Windows, Mac OS, Raspberry Pi |
| **Agent Required** | SSM agent must be installed on managed systems |

---

## 🎯 Key Takeaways

✅ **SSM is a hybrid service** – Manages both EC2 instances and on-premises systems

✅ **Fleet management at scale** – Manage entire server fleet from one place

✅ **Key capabilities:**
- Automated patching for compliance
- Run commands across entire fleet
- SSM Parameter Store for configuration
- Operational insights

✅ **SSM agent required** – Must be installed on all systems (pre-installed on Amazon Linux and some Ubuntu AMIs)

✅ **Multi-platform support** – Works with Linux, Windows, Mac OS, Raspberry Pi

---


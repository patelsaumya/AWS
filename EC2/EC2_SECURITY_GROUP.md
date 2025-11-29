# 🔐 AWS EC2 Security Groups

**Security Groups** act as the **virtual firewall** for your EC2 instances, controlling **inbound** and **outbound** network traffic.  
They are one of the most fundamental concepts in AWS networking and security.

---

## 🧭 Overview

A **Security Group (SG)** determines **what traffic is allowed** to reach your instance **(inbound)** and what traffic is allowed to **leave** your instance **(outbound)**.

- ✅ **Allow rules only** — no explicit deny rules.
- ✅ Rules can reference **IP addresses** or **other security groups**.
- 🚫 By default, **all inbound traffic is blocked**.
- ✅ By default, **all outbound traffic is allowed**.

---

## 🧱 Security Groups vs EC2 Instances

Each EC2 instance must have **at least one** security group attached.  
However:
- An **EC2 instance** can have **multiple** security groups.
- A **security group** can be attached to **multiple** instances.
- Security groups are **stateful** — if traffic is allowed in, the response is automatically allowed out.

---

## 🧩 Anatomy of a Security Group Rule

Each rule specifies:

| Field | Description | Example |
|--------|-------------|----------|
| **Type** | The kind of traffic (e.g., SSH, HTTP, HTTPS) | SSH |
| **Protocol** | Network protocol (e.g., TCP, UDP, ICMP) | TCP |
| **Port Range** | The port or ports to open | 22 |
| **Source** | The IP range or security group allowed | `203.0.113.25/32` or `0.0.0.0/0` |

### Example Rule: SSH Access
| Type | Protocol | Port | Source |
|------|-----------|------|--------|
| SSH | TCP | 22 | `203.0.113.25/32` |

This allows SSH access **only** from your computer’s IP.

---

## ⚙️ Default Behavior

| Direction | Default | Description |
|------------|----------|-------------|
| **Inbound** | ❌ Blocked | You must explicitly allow traffic. |
| **Outbound** | ✅ Allowed | All outbound connections are allowed by default. |

---

## 🧠 Security Group Scope

- Security groups are **region-specific**.  
  → Switching to another **region** requires recreating them.
- Security groups are also **VPC-specific**.  
  → A group in one VPC cannot be attached to an instance in another VPC.

---

## 🔁 Referencing Other Security Groups

Security groups can **reference** other security groups to allow inter-instance communication without using IPs.

### Example: App Server ↔ Database Server

| Instance | Security Group | Allowed Inbound From |
|-----------|----------------|----------------------|
| App Server | `sg-app` | — |
| Database Server | `sg-db` | `sg-app` |

✅ This allows any instance with `sg-app` to communicate with instances using `sg-db` on the specified ports.  
No need to manage IPs — very useful in **load-balanced** or **auto-scaled** setups.

---

## 🧰 Common Best Practices

1. **Create separate SGs for specific roles**
    - Example: one for SSH, one for web access, one for database communication.
2. **Limit SSH (port 22) to your own IP**
    - Never open `0.0.0.0/0` for SSH in production.
3. **Use security group references**
    - Easier and safer than using IP-based rules.
4. **Regularly audit** security groups
    - Remove unused ones, check for overly broad rules.
5. **Use VPC flow logs** to monitor traffic that’s allowed or denied.

---

## 🧩 Example Setup

```bash
# Inbound Rules for a Web Server
Type      Protocol   Port Range   Source
SSH       TCP        22           203.0.113.25/32
HTTP      TCP        80           0.0.0.0/0
HTTPS     TCP        443          0.0.0.0/0

# Outbound Rules
All traffic allowed (default)
```

---

## 🔢 Common Ports to Remember

| Service | Port | Protocol | Description |
|----------|------|-----------|-------------|
| **SSH** | 22 | TCP | Secure Shell for Linux server login |
| **SFTP** | 22 | TCP | Secure File Transfer Protocol |
| **FTP** | 21 | TCP | File Transfer Protocol (unsecured) |
| **HTTP** | 80 | TCP | Unsecured web traffic |
| **HTTPS** | 443 | TCP | Encrypted web traffic |
| **RDP** | 3389 | TCP | Remote Desktop Protocol for Windows instances |
| **MySQL** | 3306 | TCP | MySQL database connection |
| **PostgreSQL** | 5432 | TCP | PostgreSQL database connection |
| **Custom Application Port** | Any | TCP/UDP | Application-specific network traffic |

> 💡 **Tip:**
> - Always restrict SSH (port 22) and RDP (port 3389) to trusted IPs only.
> - Use HTTPS (443) instead of HTTP (80) in production for secure connections.

---

## 🧩 Quick Troubleshooting Guide

When your EC2 instance isn’t reachable, use this quick table to diagnose common issues:

| Symptom | Likely Cause | Recommended Fix |
|----------|--------------|-----------------|
| **Connection times out** | Inbound rule missing or wrong port open | Add correct inbound rule with proper port and IP/CIDR range |
| **Connection refused** | Service not running or wrong port configured | Verify application/service is running on the correct port |
| **Works for you but not others** | IP restriction too narrow | Check `Source` IP/CIDR in inbound rules |
| **No outbound internet** | Outbound rule too restrictive | Allow `0.0.0.0/0` for outbound traffic (default behavior) |
# 🌐 IP Addresses in AWS

## 📋 Overview

Understanding **IPv4** and **IPv6** addresses in AWS, including public, private, and Elastic IP addresses.

---

## 🔢 IPv4 Addresses

### **Public IPv4**

- **Internet-accessible** – Can be reached from anywhere on the internet
- **Dynamic assignment** – EC2 instances get a public IPv4 at launch
- **Released on stop** – IP is released when instance stops
- **New IP on restart** – Gets a new public IPv4 when instance starts again
- **Pricing:** $0.005 per hour

### **Private IPv4**

- **Private network only** – Used within internal AWS VPC
- **Not publicly accessible** – Cannot be reached from the internet
- **Format example:** `192.168.1.1`
- **Persistent** – Same IP for entire EC2 instance lifetime (even after stop/restart)
- **Free** – No charge for private IPs

### **Elastic IP (EIP)**

- **Fixed public IPv4** – Static public IP address
- **Persistent** – Same public IP even after stop/restart
- **Use case** – When you need a consistent public endpoint
- **Pricing:** $0.005 per hour (same as public IPv4)
- **Note:** Charged when allocated but not associated with a running instance

---

## 🔢 IPv6 Addresses

- **Newer protocol** – 3.4 × 10³⁸ addresses (vastly more than IPv4's 4.3 billion)
- **All public** – No private range for IPv6 in AWS
- **Format example:** `2001:0db8:85a3:0000:0000:8a2e:0370:7334`
- **Free** – No charge for IPv6 addresses
- **Use case** – Expose services publicly without IPv4 charges

---

## 🎯 Key Takeaways

✅ **IPv4:**
- **Public IPv4** – Dynamic, released on stop, new on restart, $0.005/hour
- **Private IPv4** – Persistent, private network only, free
- **Elastic IP** – Fixed public IPv4, persistent, $0.005/hour

✅ **IPv6:**
- All addresses are public
- Free in AWS
- Use for cost-effective public exposure

✅ **AWS pricing strategy:**
- Encourages IPv6 adoption (free vs. $0.005/hour for public IPv4)
- Public IPv4 addresses are charged to incentivize IPv6 migration

✅ **EC2 behavior:**
- **Public IPv4:** Changes on stop/restart
- **Private IPv4:** Remains same for instance lifetime
- **Elastic IP:** Remains same even after stop/restart

---


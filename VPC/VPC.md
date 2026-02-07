# ☁️ Virtual Private Cloud (VPC)

## 📋 Overview

**VPC (Virtual Private Cloud)** is a private network in AWS where you deploy your resources (e.g., EC2 instances). It provides isolated network environment with full control over IP addressing, routing, and security.

---

## 🏗️ Key Concepts

### **Region Association**

- **One VPC per region** – VPC is linked to a specific AWS region
- **Multiple regions = Multiple VPCs** – Each region can have its own VPC(s)

### **CIDR (Classless Inter-Domain Routing) Range**

- **IP address range** – Defines the range of IP addresses allowed within your VPC
- **Example:** `10.0.0.0/16` (65,536 IP addresses)
- **Subnetting** – VPC is divided into subnets with smaller CIDR blocks

### **Subnets**

- **Network partition** – Subnets are partitions of your VPC network
- **Availability Zone association** – Each subnet is associated with one Availability Zone
- **Types:** [Public Subnet](Subnet.md#public-subnet) and [Private Subnet](Subnet.md#private-subnet)

### **Route Tables**

- **Traffic routing** – Define how traffic flows within VPC and to/from internet
- **Subnet association** – Each subnet has a route table
- **Routes** – Define paths to internet gateways, NAT gateways, VPC peers, etc.

---

## 🏛️ VPC Architecture Example

```
AWS Cloud
└── Region (e.g., us-east-1)
    └── VPC (CIDR: 10.0.0.0/16)
        ├── AZ 1
        │   ├── Public Subnet (10.0.1.0/24)
        │   └── Private Subnet (10.0.2.0/24)
        └── AZ 2
            ├── Public Subnet (10.0.3.0/24)
            └── Private Subnet (10.0.4.0/24)
```

**Components:**
- **1 VPC** across **2 Availability Zones**
- **4 Subnets** (2 public, 2 private)
- **Route Tables** for internet connectivity
- **Internet Gateway** for public subnet access
- **NAT Gateway** for private subnet internet access

---

## 🔗 Related Components

### **[Subnets](Subnet.md)**

- **Public Subnet** – Accessible from internet, direct internet connectivity
- **Private Subnet** – Not accessible from internet, can access internet via NAT

### **[Internet Gateway](Internet_Gateway.md)**

- **Public internet access** – Enables VPC resources to connect to internet
- **Required for public subnets** – Route table directs traffic to Internet Gateway

### **[NAT Gateway](NAT_Gateway.md)**

- **Private subnet internet access** – Allows private subnet resources to access internet
- **Managed service** – AWS-managed NAT Gateway or self-managed NAT Instance
- **Architecture:** Private Subnet → NAT Gateway → Internet Gateway → Internet

### **[Network ACL & Security Groups](NACL_&_Security_Group.md)**

- **Network ACL** – Subnet-level firewall (first line of defense), supports ALLOW and DENY rules, stateless
- **Security Groups** – ENI-level firewall (second line of defense), ALLOW rules only, stateful

### **[VPC Flow Logs](Flow_Logs.md)**

- **IP traffic logging** – Capture information about IP traffic flowing through network interfaces
- **Multiple levels** – Enable at VPC, subnet, or ENI level
- **Destinations** – Send logs to S3, CloudWatch Logs, or Kinesis Data Firehose
- **Use case:** Monitor and troubleshoot connectivity issues

### **[VPC Peering](Peering.md)**

- **Private VPC connection** – Connect two VPCs privately using AWS network
- **Same network behavior** – Peered VPCs behave as if on the same network
- **Requirements:** Non-overlapping CIDR ranges, route table configuration
- **Non-transitive** – Must create direct peering connection between each pair of VPCs

### **[VPC Endpoints](Endpoints.md)**

- **Private AWS service access** – Connect to AWS services privately using AWS network
- **Gateway Endpoint** – S3 and DynamoDB only, free, uses route table
- **Interface Endpoint** – All other AWS services, paid, uses ENI
- **Benefits:** Better security, lower latency, no public internet exposure

### **[AWS PrivateLink](PrivateLink.md)**

- **Private service exposure** – Expose services in your VPC to other VPCs privately
- **Provider:** Network Load Balancer + VPC Endpoint Service
- **Consumer:** VPC Endpoint (ENI) to access provider's service
- **Benefits:** Scalable, secure, no VPC peering/internet gateway/NAT required

### **[Site-to-Site VPN](Site_to_Site_VPN.md)**

- **Hybrid cloud connection** – Connect on-premises data center to VPC over public internet (encrypted)
- **Components:** Customer Gateway (CGW) on-premises, Virtual Private Gateway (VGW) on AWS
- **Quick setup** – ~5 minutes, cost-effective, limited bandwidth

### **[AWS Client VPN](Client_VPN.md)**

- **Private computer access** – Connect your computer to VPC privately using OpenVPN
- **Private IP access** – Access EC2 instances using private IP addresses
- **On-premises access** – Can also access on-premises resources if Site-to-Site VPN is configured

### **[AWS Direct Connect](Direct_Connect.md)**

- **Physical private connection** – Dedicated physical link between on-premises and AWS over private network
- **Characteristics:** Private, secure, fast, reliable, expensive, long setup (1+ month)
- **Use case:** High bandwidth, private network requirements, compliance needs

### **[AWS Transit Gateway](Transit_Gateway.md)**

- **Hub-and-spoke model** – Central gateway connecting thousands of VPCs and on-premises systems
- **Simplifies topology** – Single gateway instead of multiple VPC peering connections
- **Connects:** VPCs, VPN connections, Direct Connect gateways
- **Use case:** Connect hundreds or thousands of VPCs together with on-premises infrastructure

---

## 🛠️ Hands-On

### **Step 1: View Default VPC**

1. Go to **VPC Console** → Click **Your VPCs**
2. **Default VPC** – AWS automatically creates one VPC per region
3. **View CIDR range:**
   - Example: `172.31.0.0/16`
   - Use CIDR calculator (e.g., cidr.xyz) to understand:
     - **First usable IP:** `172.31.0.1`
     - **Last usable IP:** `172.31.255.254`
     - **Total IPs:** 65,536 addresses
4. **Edit CIDR:** Can add more IPv4 CIDR blocks or IPv6 CIDR if needed

### **Step 2: Explore Subnets**

1. Click **Subnets** in left sidebar
2. **Default subnets** – Three subnets created automatically (one per AZ)
3. **View subnet CIDR:**
   - Example: `172.31.0.0/20` (4,096 IPs)
   - Each subnet has different CIDR (e.g., `172.31.0.0/20`, `172.31.16.0/20`, `172.31.32.0/20`)
   - **Available IPs:** 4,091 per subnet (AWS reserves 5 IPs: network address, VPC router, DNS server, reserved for future use, broadcast address)
4. **Availability Zones** – Each subnet associated with different AZ (e.g., `eu-west-1a`, `eu-west-1b`, `eu-west-1c`)

### **Step 3: Launch EC2 Instance in Subnet**

1. Go to **EC2 Console** → **Instances** → **Launch instance**
2. **Network settings:**
   - **VPC:** Default VPC (auto-selected)
   - **Subnet:** Choose specific subnet (e.g., `eu-west-1a`)
3. Launch instance (no key pair needed for demo)
4. **View private IP:**
   - Instance gets private IPv4 (e.g., `172.31.28.181`)
   - **IP matches subnet CIDR** – IP falls within chosen subnet's CIDR range
5. **Refresh subnet** – Available IPv4 addresses decrease by 1

### **Step 4: Understand Public Subnet**

1. **View public IP:**
   - Instance has **public IPv4 address** (auto-assigned)
   - This indicates instance is in a **public subnet**

2. **Check Internet Gateway:**
   - Go to **Internet Gateways** in VPC Console
   - Internet Gateway is **attached to VPC** (VPC-level resource)

3. **View Route Table:**
   - Go to **Subnets** → Select subnet → Click **Route table**
   - **Routes:**
     - `172.31.0.0/16` → `local` (VPC CIDR stays local)
     - `0.0.0.0/0` → `Internet Gateway` (all other traffic goes to internet)
   - **Subnet association:** Same route table used by all three default subnets

4. **How it works:**
   - Traffic to VPC CIDR → Stays local (private)
   - Traffic to external IPs (e.g., google.com) → Routes to Internet Gateway → Internet
   - **Route to Internet Gateway = Public subnet**

### **Step 5: Private Subnets and NAT Gateway**

1. **Private subnets:**
   - Default VPC only has **public subnets**
   - To create private subnet: Create route table **without** Internet Gateway route
   - Private subnets = No route to Internet Gateway

2. **NAT Gateway:**
   - Required for private subnet internet access (e.g., OS updates)
   - Create NAT Gateway in **public subnet**
   - Private subnet route table: `0.0.0.0/0` → `NAT Gateway`
   - NAT Gateway → Internet Gateway → Internet

### **Key Observations**

- **CIDR calculation:** Use tools like cidr.xyz to understand IP ranges
- **Private IP assignment:** IP comes from subnet's CIDR block
- **Public subnet:** Route table has `0.0.0.0/0` → Internet Gateway
- **Default VPC:** All subnets are public (have Internet Gateway route)
- **Subnet = Network partition:** Smaller CIDR block within VPC CIDR
- **Route tables:** Control internet connectivity (Internet Gateway = public, NAT Gateway = private)

---

## 🎯 Key Takeaways

✅ **VPC = Private network** for deploying AWS resources

✅ **Region-scoped** – One VPC per region (multiple regions = multiple VPCs)

✅ **CIDR range** – Defines IP address space for VPC

✅ **Subnets** – Network partitions within VPC, associated with Availability Zones

✅ **Route Tables** – Control traffic routing within VPC and to internet

✅ **Default VPC** – AWS creates a default VPC with public subnets in each region

✅ **Architecture:**
- **Public Subnet** → Direct internet access via Internet Gateway
- **Private Subnet** → Internet access via NAT Gateway (remains private)

✅ **Use cases:**
- **Public Subnet:** EC2 instances, Load Balancers
- **Private Subnet:** Databases, application servers (more secure)

---


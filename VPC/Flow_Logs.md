# 📊 VPC Flow Logs

## 📋 Overview

**VPC Flow Logs** capture information about IP traffic flowing through network interfaces in your VPC. They help monitor and troubleshoot connectivity issues.

---

## 🔑 Key Characteristics

- **Traffic logging** – Logs all IP traffic going through network interfaces
- **Multiple levels** – Can enable at VPC, subnet, or Elastic Network Interface (ENI) level
- **Monitoring and troubleshooting** – Helps identify connectivity issues
- **Multiple destinations** – Can send logs to S3, CloudWatch Logs, or Kinesis Data Firehose

---

## 🎯 Use Cases

### **Connectivity Troubleshooting**

- **Subnet to internet** – Troubleshoot why subnet cannot connect to internet
- **Subnet to subnet** – Troubleshoot connectivity between subnets
- **Internet to subnet** – Troubleshoot why internet cannot access subnet
- **Root cause analysis** – Identify the source of connectivity problems

### **Resource Coverage**

- **EC2 instances** – Monitor traffic to/from EC2 instances
- **Elastic Load Balancers** – Monitor ELB traffic
- **ElastiCache** – Monitor cache cluster traffic
- **RDS and Aurora** – Monitor database traffic
- **All VPC resources** – Any resource with a network interface

---

## 🏗️ How It Works

### **Flow Log Levels**

1. **VPC Flow Log** – Logs traffic for all network interfaces in the VPC
2. **Subnet Flow Log** – Logs traffic for all network interfaces in the subnet
3. **ENI Flow Log** – Logs traffic for a specific Elastic Network Interface

### **Log Record Format**

Each log entry includes:
- **Version** – Flow log version
- **Account ID** – AWS account ID
- **Interface ID** – Network interface ID
- **Source address** – Source IP address
- **Destination address** – Destination IP address
- **Source port** – Source port number
- **Destination port** – Destination port number
- **Protocol** – IP protocol number
- **Packets** – Number of packets
- **Bytes** – Number of bytes
- **Start** – Start time of capture window
- **End** – End time of capture window
- **Action** – ACCEPT or REJECT
- **Log status** – Status of the log record

---

## 🔧 Configuration

### **Flow Log Settings**

1. **Filter:**
   - **All traffic** – Log all traffic
   - **Accepted traffic** – Log only accepted traffic
   - **Rejected traffic** – Log only rejected traffic

2. **Aggregation interval:**
   - **1 minute** – More granular logging
   - **10 minutes** – Less granular, lower cost

3. **Destination:**
   - **CloudWatch Logs** – Requires log group and IAM role
   - **Amazon S3** – Requires S3 bucket
   - **Kinesis Data Firehose** – Can send to same or different account

---

## 🛠️ Hands-On

### **Step 1: Create Flow Log**

1. Go to **VPC Console** → Select **VPC** → Click **Flow logs** tab
2. Click **Create flow log**
3. **Configure settings:**
   - **Name:** Enter flow log name
   - **Filter:** Choose All traffic, Accepted traffic, or Rejected traffic
   - **Maximum aggregation interval:** 1 minute or 10 minutes
   - **Destination:** Choose CloudWatch Logs, S3, or Kinesis Data Firehose

### **Step 2: Configure Destination**

**For CloudWatch Logs:**
- Specify **Log group**
- Provide **IAM role** (for CloudWatch Logs permissions)

**For S3:**
- Specify **S3 bucket** (can be in same or different account)

**For Kinesis Data Firehose:**
- Specify **Delivery stream** (can be in same or different account)

### **Step 3: View Log Record Format**

- **Log record format** shows fields included in each log entry
- Includes: version, account ID, interface ID, source/destination addresses and ports, protocol, packets, bytes, timestamps, action, log status

### **Key Observations**

- **Flow logs = Traffic monitoring** – Capture all IP traffic through network interfaces
- **Multiple levels** – Can enable at VPC, subnet, or ENI level
- **Multiple destinations** – S3, CloudWatch Logs, or Kinesis Data Firehose
- **Filtering options** – All, accepted, or rejected traffic
- **Use case:** Troubleshoot connectivity issues (subnet to internet, subnet to subnet, etc.)

---

## 🎯 Key Takeaways

✅ **VPC Flow Logs = IP traffic logging** for network interfaces

✅ **Three levels:**
- **VPC level** – All network interfaces in VPC
- **Subnet level** – All network interfaces in subnet
- **ENI level** – Specific Elastic Network Interface

✅ **Use cases:**
- Monitor and troubleshoot connectivity issues
- Subnet to internet connectivity
- Subnet to subnet connectivity
- Internet to subnet access

✅ **Resources covered:**
- EC2 instances, ELB, ElastiCache, RDS, Aurora, all VPC resources

✅ **Destinations:**
- **CloudWatch Logs** – Requires log group and IAM role
- **Amazon S3** – Simple storage
- **Kinesis Data Firehose** – Can send to same or different account

✅ **Configuration:**
- **Filter:** All, accepted, or rejected traffic
- **Aggregation interval:** 1 minute or 10 minutes
- **Log format:** Includes source/destination, ports, protocol, packets, bytes, action, etc.

---


# 📁 Amazon EFS (Elastic File System)

## 📋 Overview

**Amazon EFS (Elastic File System)** is a managed network file system (NFS) that provides scalable, shared file storage for EC2 instances. Unlike EBS volumes, which can only be attached to one instance at a time, EFS can be mounted to hundreds of EC2 instances simultaneously, making it ideal for shared storage scenarios across multiple instances and Availability Zones.

---

## 🔍 What is EFS?

**EFS (Elastic File System)** is a managed network file system that provides shared file storage accessible by multiple EC2 instances at the same time. It uses the Network File System (NFS) protocol and is designed for scenarios where multiple instances need to access the same files concurrently.

### 🔑 Key Characteristics

- **Shared file system** – Can be mounted to hundreds of EC2 instances simultaneously
- **Network file system (NFS)** – Uses standard NFS protocol for file access
- **Multi-AZ support** – Works across multiple Availability Zones
- **Linux only** – Works exclusively with Linux EC2 instances
- **Highly available** – Built-in redundancy and high availability
- **Scalable** – Automatically scales as you add or remove files
- **Pay per use** – No capacity planning required; pay only for what you store

---

## ⚙️ How EFS Works

### 🌐 Multi-Instance Mounting

EFS file systems can be mounted to multiple EC2 instances across different Availability Zones:

- **Same file system** – All instances see the same files and directories
- **Concurrent access** – Multiple instances can read and write to the same files simultaneously
- **Mount targets** – Instances connect to EFS through mount targets in each Availability Zone
- **Security groups** – EFS file systems use security groups to control access

### 📍 Cross-AZ Architecture

EFS works across multiple Availability Zones:

- **Single file system** – One EFS file system can serve instances in multiple AZs
- **Automatic replication** – Data is automatically replicated across AZs for high availability
- **No AZ binding** – Unlike EBS, EFS is not bound to a specific Availability Zone
- **Regional service** – EFS file systems exist at the region level

---

## 💰 Pricing

EFS pricing characteristics:

- **Expensive** – Approximately **3 times the price** of a gp2 EBS volume
- **Pay per use** – You only pay for the storage you actually use
- **No capacity planning** – No need to provision capacity in advance
- **Example** – If you store 20 GB of data, you only pay for those 20 GB

> 💡 **Cost Consideration:** While EFS is more expensive than EBS, it provides shared access and automatic scaling, which can be valuable for certain use cases.

---

## 🔄 EFS vs EBS Comparison

### 📊 Key Differences

| Feature | EBS | EFS |
|---------|-----|-----|
| **Attachment** | One instance at a time | Hundreds of instances simultaneously |
| **Availability Zone** | Bound to specific AZ | Works across multiple AZs |
| **Type** | Block storage | Network file system (NFS) |
| **Sharing** | Not shared (one instance only) | Shared file system |
| **Cross-AZ** | Requires snapshot and restore (copy) | Native multi-AZ support |
| **Instance OS** | Linux and Windows | Linux only |
| **Pricing** | Lower cost (gp2 baseline) | ~3x more expensive than gp2 |
| **Capacity** | Provisioned in advance | Pay per use, no provisioning |
| **Use Case** | Single instance storage | Shared storage across multiple instances |

### 🔍 Detailed Comparison

**EBS Volumes:**
- Can only be attached to **one EC2 instance** at a time
- Bound to a **specific Availability Zone**
- To move across AZs, you must create a **snapshot** and restore it (creates a copy, not a live replica)
- Each instance needs its own EBS volume if they need separate storage

**EFS File Systems:**
- Can be mounted to **hundreds of EC2 instances** simultaneously
- Works **across multiple Availability Zones**
- All instances see the **same files** in real-time (truly shared)
- Single file system serves all instances

---

## 🏷️ EFS Storage Classes

EFS offers different storage classes optimized for different access patterns:

### 📦 EFS Standard

- **Default storage class** – Used for frequently accessed files
- **Higher cost** – Standard pricing tier
- **Immediate access** – No retrieval delays

### 💾 EFS Infrequent Access (EFS-IA)

- **Cost-optimized** – Up to **92% lower cost** compared to EFS Standard
- **Automatic lifecycle management** – Files are automatically moved based on access patterns
- **Lifecycle policy** – Configure when files should be moved to EFS-IA (e.g., after 60 days of no access)
- **Transparent to applications** – Applications access files the same way regardless of storage class
- **Automatic promotion** – Files are moved back to EFS Standard when accessed again

### 🔄 Lifecycle Policy Example

1. **File in EFS Standard** – File hasn't been accessed for 60 days
2. **Automatic move** – EFS lifecycle policy moves the file to EFS-IA
3. **Cost savings** – File now stored at 92% lower cost
4. **Access triggers promotion** – When the file is accessed again, it's automatically moved back to EFS Standard
5. **Transparent operation** – Applications don't need to know which storage class the file is in

### ⚙️ Lifecycle Policy Configuration

- **Access-based** – Move files based on last access time
- **Configurable threshold** – Set the number of days (e.g., 60 days) before moving to EFS-IA
- **Automatic operation** – No manual intervention required
- **Cost optimization** – Significant cost savings for infrequently accessed files

---

## 🎯 Use Cases

EFS is ideal for:

- **Content management systems** – Shared content across multiple web servers
- **Application deployment** – Shared application code and configuration files
- **Data analytics** – Shared datasets accessible by multiple compute instances
- **Web serving** – Shared web content across multiple web servers
- **Development environments** – Shared code repositories and build artifacts
- **Media processing** – Shared media files for processing workflows
- **Home directories** – Shared user home directories

---

## ✅ Best Practices

1. **Enable EFS-IA** – Use lifecycle policies to automatically move infrequently accessed files to EFS-IA for cost savings
2. **Security groups** – Configure EFS security groups to allow access only from authorized EC2 instances
3. **Mount targets** – Create mount targets in each Availability Zone where you have instances
4. **Performance mode** – Choose the appropriate performance mode (General Purpose or Max I/O) based on your workload
5. **Throughput mode** – Select Bursting or Provisioned throughput mode based on your needs
6. **Monitor usage** – Track file access patterns to optimize lifecycle policies
7. **Cost optimization** – Use EFS-IA for files that are accessed infrequently

---

## 📊 Summary

| Concept | Description |
|---------|-------------|
| **Type** | Managed network file system (NFS) |
| **Mounting** | Can mount to hundreds of EC2 instances simultaneously |
| **Sharing** | Shared file system - all instances see the same files |
| **Availability Zones** | Works across multiple AZs (not bound to one AZ) |
| **Instance OS** | Linux EC2 instances only |
| **Pricing** | ~3x more expensive than gp2 EBS, pay per use |
| **Capacity** | No capacity planning - pay for what you use |
| **Storage Classes** | EFS Standard and EFS-IA (92% cost savings) |
| **Lifecycle Policy** | Automatically moves files between storage classes |
| **High Availability** | Built-in redundancy and multi-AZ support |

---

## 🎯 Key Takeaways

- EFS is a **shared network file system** that can be mounted to hundreds of EC2 instances at once
- Works **across multiple Availability Zones** - instances in different AZs can mount the same EFS file system
- **Linux only** - Works exclusively with Linux EC2 instances
- **More expensive** than EBS (~3x gp2 pricing) but provides shared access and automatic scaling
- **Pay per use** - No capacity planning needed; pay only for the storage you actually use
- **EFS-IA storage class** offers up to 92% cost savings for infrequently accessed files
- **Lifecycle policies** automatically move files between storage classes based on access patterns
- **Transparent to applications** - Applications don't need to know which storage class files are in
- Ideal for scenarios requiring **shared file storage** across multiple instances


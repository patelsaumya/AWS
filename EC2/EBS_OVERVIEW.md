# 💾 Amazon EBS (Elastic Block Store)

## 📋 Overview

**Amazon EBS (Elastic Block Store)** is a network-attached storage service that provides persistent block-level storage volumes for use with Amazon EC2 instances. EBS volumes are one of the primary storage options for EC2 instances, allowing you to persist data even after an instance is terminated.

---

## 🔍 What is EBS?

**EBS volumes** are network drives that you can attach to your EC2 instances while they run. Think of them as **network USB sticks**—you can detach them from one instance and attach them to another, but the attachment happens over the network rather than physically.

### 🔑 Key Characteristics

- **Network-attached storage** – EBS volumes are not physical drives attached directly to your instance; they communicate over the network
- **Persistent storage** – Data persists even after the instance is terminated
- **Detachable and reattachable** – Volumes can be detached from one instance and attached to another, making them useful for failover scenarios
- **Availability Zone bound** – EBS volumes are created in a specific Availability Zone (AZ) and can only be attached to instances in the same AZ
- **Provisioned capacity** – You must provision capacity in advance (size in GB and IOPS)

---

## ⚙️ How EBS Works

### 🌐 Network Drive Architecture

EBS volumes are network drives, which means:
- Communication between the instance and the EBS volume occurs over the network
- There may be some latency compared to physical drives, but it's typically minimal
- Volumes can be quickly detached and reattached to different instances

### 📍 Availability Zone Binding

EBS volumes are **locked to a specific Availability Zone**:
- If you create a volume in `us-east-1a`, it can only be attached to instances in `us-east-1a`
- You cannot attach a volume from one AZ to an instance in a different AZ
- To move a volume across AZs, you must create a **snapshot** and restore it in the target AZ

### 🔌 Volume Attachment

- **Single instance attachment (default)** – By default, EBS volumes can only be attached to one EC2 instance at a time
- **Multi-attach (io1/io2 volumes)** – Some EBS volume types support attaching a single volume to multiple instances in the same AZ
- **Multiple volumes per instance** – A single EC2 instance can have multiple EBS volumes attached to it simultaneously

---

## ⚙️ EBS Volume Configuration

### 📊 Provisioned Capacity

When creating an EBS volume, you need to specify:

1. **Size (in GB)** – The storage capacity you want to provision
2. **IOPS (Input/Output Operations Per Second)** – The performance level for your volume
3. **Volume Type** – The type of EBS volume (gp2, gp3, io1, io2, etc.)

You are billed for the provisioned capacity, regardless of how much data you actually store. You can increase capacity over time to improve performance or add more storage.

### 🗑️ Delete on Termination

When creating an EBS volume through the EC2 console, you'll see a **"Delete on Termination"** attribute:

- **Root volume** – By default, the root volume has "Delete on Termination" **enabled**, meaning it will be deleted when the instance is terminated
- **Additional volumes** – By default, additional EBS volumes have "Delete on Termination" **disabled**, so they persist after instance termination

You can modify this setting to:
- Preserve the root volume when an instance is terminated (disable delete on termination)
- Automatically delete additional volumes when an instance is terminated (enable delete on termination)

---

## 📸 EBS Snapshots

### 📋 Overview

**EBS snapshots** are point-in-time backups of your EBS volumes. You can create a snapshot of your EBS volume at any point in time, capturing the exact state of the volume at that moment. Even if the original EBS volume is terminated later, you can restore it from the snapshot backup.

### 🎯 Why Use Snapshots?

- **Backup and recovery** – Restore volumes from snapshots if data is lost or corrupted
- **Cross-AZ migration** – Copy snapshots across Availability Zones to move volumes between AZs
- **Cross-region migration** – Copy snapshots across AWS regions to leverage global infrastructure
- **Disaster recovery** – Maintain backups in different regions for business continuity

### 🔄 Creating Snapshots

- **No detachment required** – You can create snapshots while the volume is attached to an instance
- **Recommended practice** – While not required, it's recommended to stop the EC2 instance or detach the volume before creating a snapshot to ensure data consistency
- **On-the-fly snapshots** – You can create snapshots while the instance is running, but this depends on how your application handles concurrent access

### 🌐 Moving Volumes Across Availability Zones

Since EBS volumes are bound to a specific Availability Zone, snapshots are the primary method to move volumes between AZs:

1. **Create a snapshot** of the EBS volume in the source AZ (e.g., `us-east-1a`)
2. **Snapshots exist at the region level** – The snapshot is stored in your AWS region
3. **Restore from snapshot** – Create a new EBS volume from the snapshot in the target AZ (e.g., `us-east-1b`)
4. **Attach to instance** – Attach the new volume to an EC2 instance in the target AZ

This process effectively transfers your EBS volume data across Availability Zones.

### 💾 EBS Snapshot Archive

**EBS Snapshot Archive** allows you to move snapshots to a lower-cost storage tier:

- **Cost savings** – Archive tier is **75% cheaper** than standard snapshot storage
- **Restore time** – Takes **24 to 72 hours** to restore from the archive tier
- **Use case** – Ideal for snapshots that you don't need to restore quickly but want to keep for long-term retention
- **Manual or automated** – You can move snapshots to archive manually or set up automated policies

> 💡 **Best Practice:** Use archive tier for compliance snapshots, long-term backups, or snapshots that are rarely accessed.

### 🗑️ Recycle Bin for EBS Snapshots

**Recycle Bin** protects against accidental deletion of EBS snapshots:

- **Default behavior** – By default, when you delete snapshots, they are permanently deleted
- **Recycle bin protection** – When enabled, deleted snapshots go into the recycle bin instead of being immediately deleted
- **Retention period** – You can configure retention from **1 day to 1 year**
- **Recovery window** – During the retention period, you can recover snapshots from the recycle bin
- **Automatic deletion** – After the retention period expires, snapshots are permanently deleted from the recycle bin

> 💡 **Best Practice:** Enable recycle bin with an appropriate retention period to protect against accidental deletions while managing costs.

---

## 🔀 EBS Multi-Attach

### 📋 Overview

**EBS Multi-Attach** allows you to attach a single EBS volume to multiple EC2 instances in the same Availability Zone. This feature is available for **Provisioned IOPS SSD (io1 and io2)** volumes.

### 🎯 Use Cases

- **High availability applications** – Multiple instances can access the same data simultaneously
- **Clustered applications** – Applications that require shared storage across multiple nodes
- **Faster failover** – No need to detach and reattach volumes when switching between instances

### ⚠️ Important Considerations

- **File system compatibility** – The file system on the volume must support concurrent access (e.g., cluster-aware file systems)
- **Same Availability Zone only** – All instances must be in the same AZ as the volume
- **Volume type requirement** – Only io1 and io2 volumes support multi-attach
- **Maximum attachments** – Up to 16 instances can attach to a single multi-attach volume

### ⚠️ Limitations

- **Not for all workloads** – Standard file systems (like ext4, xfs) are not cluster-aware and may corrupt data if multiple instances write simultaneously
- **Use cluster file systems** – Requires file systems designed for concurrent access, such as:
  - GFS2 (Global File System 2)
  - OCFS2 (Oracle Cluster File System 2)
  - Other cluster-aware file systems

---

## 🏷️ EBS Volume Types

EBS offers several volume types optimized for different use cases:

| Volume Type | Description | Use Cases |
|------------|-------------|-----------|
| **gp2/gp3** | General Purpose SSD | Boot volumes, small to medium databases, development and test environments |
| **io1/io2** | Provisioned IOPS SSD | I/O-intensive applications, large databases, multi-attach scenarios |
| **st1** | Throughput Optimized HDD | Big data, data warehouses, log processing |
| **sc1** | Cold HDD | Throughput-oriented workloads with infrequent access |

---

## ✅ Best Practices

1. **Snapshots for backup** – Regularly create snapshots of your EBS volumes for backup and disaster recovery
2. **Snapshot for cross-AZ migration** – Use snapshots to move volumes between Availability Zones
3. **Right-size your volumes** – Monitor your actual usage and adjust volume size and IOPS accordingly
4. **Enable encryption** – Use EBS encryption for sensitive data
5. **Monitor performance** – Use CloudWatch to monitor volume performance and optimize as needed

---

## 📊 Summary

| Concept | Description |
|---------|-------------|
| **Type** | Network-attached block storage |
| **Persistence** | Data persists after instance termination |
| **Availability Zone** | Bound to a specific AZ (can move via snapshots) |
| **Attachment** | Single instance (default) or multi-attach (io1/io2) |
| **Provisioning** | Capacity (size and IOPS) must be provisioned in advance |
| **Billing** | Based on provisioned capacity |
| **Delete on Termination** | Configurable per volume (enabled by default for root volume) |
| **Snapshots** | Point-in-time backups for recovery and cross-AZ/region migration |
| **Snapshot Archive** | 75% cheaper storage tier with 24-72 hour restore time |
| **Recycle Bin** | Protection against accidental snapshot deletion (1 day to 1 year retention) |

---

## 🎯 Key Takeaways

- EBS volumes are **persistent network drives** that can be attached to EC2 instances
- Volumes are **bound to a specific Availability Zone** but can be moved via snapshots
- **Snapshots** provide point-in-time backups and enable cross-AZ/region volume migration
- **Snapshot Archive** offers 75% cost savings for long-term retention (24-72 hour restore time)
- **Recycle Bin** protects against accidental snapshot deletion with configurable retention (1 day to 1 year)
- **Multi-attach** is available for io1/io2 volumes, allowing shared storage across multiple instances
- You **provision capacity in advance** and are billed for what you provision
- **Delete on Termination** controls whether volumes are deleted when instances terminate


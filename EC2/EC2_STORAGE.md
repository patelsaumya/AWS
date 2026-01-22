# 💾 EC2 Storage Options

## 📋 Overview

EC2 instances support multiple storage options, each designed for different use cases and performance requirements. Understanding the various storage types and their characteristics is essential for choosing the right solution for your workloads.

---

## 🔗 EC2 Storage Documentation

This document provides an overview of EC2 storage options. For detailed information on each storage type, refer to the following documentation:

- **[AMI (Amazon Machine Image)](AMI_OVERVIEW.md)** – Templates that define the software configuration for EC2 instances
- **[EBS (Elastic Block Store)](EBS_OVERVIEW.md)** – Network-attached block storage volumes for EC2 instances
- **[EFS (Elastic File System)](EFS_OVERVIEW.md)** – Managed network file system (NFS) for shared file storage
- **[FSx](FSx_OVERVIEW.md)** – Managed third-party high-performance file systems (Windows File Server and Lustre)
- **[EC2 Instance Store](EC2_INSTANCE_STORE_OVERVIEW.md)** – Ephemeral storage physically attached to the host server
- **[EC2 Image Builder](EC2_IMAGE_BUILDER_OVERVIEW.md)** – Service for automating AMI creation, maintenance, and testing

---

## 📊 Storage Options Comparison

| Storage Type | Attachment | Persistence | Sharing | Use Case |
|--------------|------------|-------------|---------|----------|
| **EBS** | Network-attached | Persistent | Single instance | Long-term storage, databases |
| **EFS** | Network file system | Persistent | Multiple instances | Shared file storage, content management |
| **FSx** | Network file system | Persistent | Multiple instances | Windows file server, HPC workloads |
| **Instance Store** | Physical hardware | Ephemeral | Single instance | Temporary data, cache, high-performance workloads |
| **AMI** | Template | N/A | N/A | Instance configuration template |

---

## ⛑️ Shared Responsibility Model for EC2 Storage

Understanding the shared responsibility model is crucial for the Certified Cloud Practitioner exam. This model defines what AWS is responsible for versus what you, as the customer, are responsible for regarding EC2 storage.

### 🔹 AWS Responsibilities

AWS is responsible for:

- **Infrastructure** – Physical infrastructure, data centers, and hardware
- **Data replication** – AWS is responsible for replicating data across multiple hardware devices as specified in the technical specifications of EBS and EFS
  - This ensures that if hardware fails, you as a customer are not impacted
  - Data redundancy is handled automatically by AWS
- **Hardware replacement** – If an EBS drive fails or any part of it fails, AWS is responsible for replacing the faulty hardware
- **Data access protection** – AWS is responsible for ensuring that their employees cannot access your data
  - AWS implements security measures to prevent unauthorized access to customer data
- **Service availability** – Maintaining the availability and reliability of storage services

### 🔹 Customer Responsibilities

You are responsible for:

- **Backup and snapshot procedures** – Setting up backup or snapshot procedures and guidelines is very important to ensure you don't lose your data
  - Create regular EBS snapshots
  - Implement backup strategies for EFS file systems
  - Document and test your backup and recovery procedures
- **Data encryption** – Setting up data encryption is another layer of protection to ensure people cannot access your data
  - Encrypt EBS volumes at rest
  - Encrypt data in transit
  - Manage encryption keys
  - This provides an additional security layer beyond AWS's built-in protections
- **Data on drives** – Any data you store on the drives is your responsibility
  - Anything you write to the disk is your own responsibility
  - You must ensure data integrity and compliance
- **Instance Store risks** – If you're using EC2 Instance Store, you need to understand the risks:
  - **Hardware failure** – You can lose the drive if there's faulty hardware
  - **Instance lifecycle** – If you stop or terminate an EC2 instance that has Instance Store, the data will be lost
  - You are responsible for backing up and replicating Instance Store data if needed

---

## 🎯 Key Takeaways

- **AWS handles infrastructure** – Physical hardware, replication, and hardware replacement
- **You handle data management** – Backups, encryption, and data protection strategies
- **Instance Store requires special attention** – Higher risk of data loss, requires your own backup strategy
- **Encryption is your responsibility** – While AWS provides the tools, you must configure and manage encryption
- **Backup procedures are critical** – Regular snapshots and backups are essential for data protection

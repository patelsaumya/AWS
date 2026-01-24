# 🪣 Amazon S3 (Simple Storage Service)

## 📋 Overview

**Amazon S3** is one of the main building blocks of AWS, providing infinitely scaling storage that serves as the backbone for much of the web. Many websites and AWS services rely on S3 for integration and storage needs. S3 is advertised as infinitely scaling storage, making it a fundamental service that powers countless applications and services worldwide.

---

## 🌐 Importance of Amazon S3

### 🏗️ Foundation of AWS

- **Main building block** – One of the core services that many other AWS services depend on
- **Web backbone** – Many websites use Amazon S3 as their storage foundation
- **Service integration** – Numerous AWS services integrate with S3 for data storage and processing
- **Infinite scalability** – Can store virtually unlimited amounts of data

---

## 🎯 Use Cases

Amazon S3 has numerous use cases because at its core, it provides reliable, scalable storage:

### 💾 Backup and Storage
- **File backup** – Store files, documents, and data safely
- **Disk storage** – Store disk images and system backups
- **Data preservation** – Long-term storage of important information

### 🚨 Disaster Recovery
- **Cross-region backup** – Move data to different regions for redundancy
- **Business continuity** – Ensure data availability even if one region goes down
- **Recovery planning** – Store critical data for disaster recovery scenarios

### 📦 Archival
- **Long-term storage** – Archive files for extended periods
- **Cost-effective retrieval** – Store data cheaply and retrieve when needed
- **Compliance** – Meet regulatory requirements for data retention

### 🔄 Hybrid Cloud Storage
- **On-premises extension** – Expand existing on-premises storage to the cloud
- **Cloud migration** – Gradually move data from on-premises to AWS
- **Flexible architecture** – Bridge between local and cloud storage
- **AWS Storage Gateway** – Hybrid cloud service connecting on-premises environments to S3 for seamless cloud integration

### 🎥 Media and Content
- **Application hosting** – Host web applications and their assets
- **Media storage** – Store videos, images, and multimedia content
- **Content delivery** – Serve static content to users worldwide

### 📊 Big Data and Analytics
- **Data lakes** – Store vast amounts of structured and unstructured data
- **Big data analytics** – Provide data source for analytics tools and services
- **Business intelligence** – Store data for reporting and analysis

### 🔄 Software and Updates
- **Software distribution** – Deliver software updates and patches
- **Version control** – Store different versions of applications
- **Content delivery** – Distribute software efficiently

### 🌐 Website Hosting
- **Static websites** – Host static websites directly from S3
- **Web assets** – Store CSS, JavaScript, images, and other web resources
- **Global delivery** – Serve content to users worldwide

---

## 🏢 Real-World Examples

### 📈 NASDAQ
- **Use case:** Data archival and compliance
- **Implementation:** Stores **7 years of data** in S3 Glacier
- **Service:** Uses S3 Glacier (archival service) for cost-effective long-term storage

### 🔍 Sysco
- **Use case:** Business analytics and insights
- **Implementation:** Runs analytics on business data stored in S3
- **Benefit:** Gains valuable business insights from stored data

---

## 🪣 S3 Buckets

### 🔍 What are Buckets?

**Buckets** are containers for storing objects (files) in Amazon S3. Think of them as **top-level directories** that organize your data.

### 🌐 Global Uniqueness

**Bucket names must be globally unique**:
- **Across all regions** – Unique across every AWS region
- **Across all accounts** – Unique across every AWS account worldwide
- **Only globally unique resource** – Buckets are the only AWS resource requiring global name uniqueness

### 📍 Regional Definition

Despite global naming requirements:
- **Created in specific regions** – Each bucket is created in a specific AWS region
- **Regional service** – Although S3 appears global, buckets are regional resources
- **Common beginner mistake** – Thinking S3 is entirely global when buckets are region-specific

---

## 📝 Bucket Naming Convention

S3 bucket names must follow specific rules:

### ✅ Requirements

- **No uppercase letters** – All lowercase characters only
- **No underscores** – Use hyphens instead of underscores
- **Length:** Between **3 and 63 characters**
- **Not an IP address** – Cannot be formatted like an IP address
- **Start with:** Lowercase letter or number
- **Safe characters:** Letters, numbers, and hyphens

### 🎯 Best Practices

- Use **letters, numbers, and hyphens** for compatibility
- Keep names **descriptive** but **concise**
- Consider **DNS compatibility** for website hosting
- Avoid **periods** in bucket names for SSL compatibility

---

## 📄 S3 Objects

### 🔍 What are Objects?

**Objects** are the files you store in S3 buckets. Each object consists of:
- **File data** – The actual content/body of the file
- **Key** – The unique identifier/path for the object
- **Metadata** – Additional information about the object

---

## 🔑 Object Keys

### 📋 Definition

An **S3 object key** is the **full path** of your file within the bucket.

### 🌐 Key Structure Examples

**Simple key (root level):**
```
Bucket: my-bucket
Key: myfile.txt
Full path: s3://my-bucket/myfile.txt
```

**Nested key (with "folders"):**
```
Bucket: my-bucket  
Key: myfolder1/anotherfolder/myfile.txt
Full path: s3://my-bucket/myfolder1/anotherfolder/myfile.txt
```

### 📂 Key Components

Keys are composed of two parts:

1. **Prefix** – The "directory" path (e.g., `myfolder1/anotherfolder/`)
2. **Object name** – The actual file name (e.g., `myfile.txt`)

### ⚠️ Important Concept: No True Directories

- **No real directories** – S3 doesn't have traditional folder structures
- **Keys are paths** – Everything is stored as keys with forward slashes
- **UI creates illusion** – The console shows "folders" but they're just key prefixes
- **Long key names** – Keys are simply very long names that contain slashes

> 💡 **Key Insight:** When you see "folders" in the S3 console, you're actually seeing key prefixes that create the appearance of a directory structure.

---

## 📊 Object Properties

### 💾 Object Size and Content

- **Value/Body** – The actual content of the file you upload
- **Maximum size** – **5 terabytes** (5,000 GB) per object
- **Large file uploads** – Files > 5 GB must use **multi-part upload**

#### 🔄 Multi-Part Upload

For files larger than 5 GB:
- **Required** – Must use multi-part upload process
- **Example** – 5 TB file = minimum 1,000 parts of 5 GB each
- **Benefits** – Faster uploads, resume capability, parallel processing

### 🏷️ Metadata

**System or user-defined key-value pairs:**
- **System metadata** – Set automatically by S3 (content-type, last-modified, etc.)
- **User metadata** – Custom information you define
- **Use cases** – File descriptions, processing instructions, custom attributes

### 🏷️ Tags

- **Unicode key-value pairs** – Up to **10 tags** per object
- **Security** – Used for access control and policies
- **Lifecycle management** – Automate object transitions and deletions
- **Cost allocation** – Track costs by tags

### 🔢 Version ID

- **Versioning enabled** – Objects get unique version IDs
- **Version tracking** – Keep multiple versions of the same object
- **Data protection** – Prevent accidental overwrites and deletions

---

## 🔍 IAM Access Analyzer for Amazon S3

### 📋 Overview

**IAM Access Analyzer for S3** is a security monitoring feature that helps ensure only intended users have access to your S3 buckets. This tool analyzes your S3 access configurations and identifies potential security issues, making it easier to maintain proper access controls.

### 🔎 How It Works

**Analysis Process:**
1. **Scans S3 configurations** across your AWS account
2. **Analyzes access policies** including bucket policies, ACLs, and access point policies  
3. **Identifies sharing patterns** with external entities
4. **Reports findings** for your security review

### 📋 What It Analyzes

**Configuration Types:**
- **S3 Bucket Policies** – JSON policies that grant access to buckets
- **S3 Access Control Lists (ACLs)** – Legacy access control mechanism
- **S3 Access Point Policies** – Policies for S3 access points
- **Cross-account sharing** – Resources shared with other AWS accounts

### 🚨 Findings and Alerts

**Types of Access Issues Detected:**

#### 🌐 Public Access
- **Publicly accessible buckets** – Buckets accessible from the internet
- **Public read/write permissions** – Unintended public access to objects
- **Open bucket policies** – Policies that allow broad public access

#### 🔄 Cross-Account Sharing
- **Shared with other AWS accounts** – Buckets accessible by external AWS accounts
- **Cross-account roles** – Access granted through IAM roles in other accounts
- **External entity access** – Any access granted outside your organization

### ✅ Review and Response Process

**Security Review Workflow:**
1. **Receive findings** from Access Analyzer
2. **Review each finding** to determine if access is intentional
3. **Classify findings:**
   - **Expected/Normal** – Intentional sharing that should remain
   - **Security Issue** – Unintended access that needs correction
4. **Take corrective action** for unintended access

### 🛡️ Security Benefits

**Proactive Security:**
- **Continuous monitoring** – Ongoing analysis of S3 access configurations
- **Early detection** – Identify access issues before they become problems
- **Compliance support** – Help maintain security compliance requirements
- **Audit trail** – Track and document access permissions

### 🔧 Powered by IAM Access Analyzer

**Underlying Technology:**
- **IAM Access Analyzer engine** – Uses the same technology as general IAM Access Analyzer
- **Resource sharing detection** – Finds resources shared with external entities
- **Comprehensive analysis** – Analyzes all access mechanisms systematically

### 🎯 Use Cases

**Security Scenarios:**
- **Regular security audits** – Periodic review of S3 access permissions
- **Compliance validation** – Ensure S3 access meets organizational policies
- **Incident investigation** – Understand how sensitive data might be exposed
- **Access hygiene** – Clean up unnecessary or excessive permissions

### 💡 Best Practices

**Recommended Actions:**
- **Regular review** – Check Access Analyzer findings regularly
- **Document intended sharing** – Maintain records of authorized cross-account sharing
- **Principle of least privilege** – Grant only the minimum necessary access
- **Automate responses** – Set up processes to address common findings

---

## 📊 Summary

| Concept | Description |
|---------|-------------|
| **Service Type** | Infinitely scaling object storage |
| **Global Scope** | Service appears global, buckets are regional |
| **Bucket Names** | Must be globally unique across all AWS accounts |
| **Objects** | Files stored in buckets with unique keys |
| **Keys** | Full path identifiers (prefix + object name) |
| **Max Object Size** | 5 terabytes per object |
| **Multi-part Upload** | Required for files > 5 GB |
| **Metadata** | System and user-defined key-value pairs |
| **Tags** | Up to 10 Unicode key-value pairs per object |
| **Versioning** | Optional version tracking with unique IDs |

---

## 🧪 Hands-On: Creating Your First S3 Bucket

### 📋 Overview

Creating an S3 bucket and uploading objects to understand the fundamental S3 concepts and operations.

---

### 📝 Step 1: Create an S3 Bucket

#### 1️⃣ Navigate to S3 Console

1. **Go to AWS Console** → **S3 Service**
2. **Select your region** (e.g., Europe Stockholm `eu-north-1`)
   - Note: S3 shows buckets from all regions, but each bucket is created in a specific region

#### 2️⃣ Choose Bucket Type (if available)

If you see bucket type options:
- **Choose:** `General Purpose` (recommended)
- **Skip if not shown:** Some regions don't show this option - that's fine, it defaults to General Purpose

> 💡 **Note:** Directory buckets are for specific use cases not covered in basic exams.

#### 3️⃣ Choose a Unique Bucket Name

**Bucket naming considerations:**
- Must be **globally unique** across all AWS accounts and regions
- Use personal/organizational identifiers to ensure uniqueness

**Example naming pattern:**
```
yourname-demo-s3-v1
company-project-s3-2024
```

**Test name availability:**
1. Enter your bucket name
2. If you get an error about name already existing, try a different variation
3. Continue when you find an available name

#### 4️⃣ Configure Bucket Settings (Use Defaults)

**Object Ownership:**
- **Setting:** ACLs disabled ✅ (Recommended)
- **Why:** Enhanced security setting

**Block Public Access:**
- **Setting:** Block all public access ✅ (Enabled)
- **Why:** Maximum security - only you can upload files

**Bucket Versioning:**
- **Setting:** Disable ❌ (for now)
- **Why:** We'll explore versioning later

**Tags:**
- **Setting:** None needed for demo

**Default Encryption:**
- **Setting:** Server-side encryption with Amazon S3 managed keys (SSE-S3)
- **Bucket Key:** Enable ✅
- **Why:** All objects automatically encrypted

#### 5️⃣ Create the Bucket

1. **Review settings** (most should be defaults)
2. **Create bucket**
3. **Verify success** → Bucket appears in S3 console

> ✅ **Expected Result:** Bucket successfully created and visible in S3 console showing buckets from all regions.

---

### 📝 Step 2: Upload Objects to Your Bucket

#### 1️⃣ Access Your Bucket

1. **Find your bucket** in the S3 console (use search if you have many buckets)
2. **Click on bucket name** to open it
3. **Verify:** Shows "0 objects" initially

#### 2️⃣ Upload Your First Object

1. **Click "Upload"**
2. **Add files** → **Browse and select a file** (e.g., an image file like `coffee.jpg`)
3. **Review file details:**
   - File type (e.g., JPG)
   - File size (e.g., 100 KB)
   - Destination bucket

4. **Click "Upload"**
5. **Wait for completion** → **Close upload panel**

> ✅ **Expected Result:** File appears in your bucket's object list.

---

### 📝 Step 3: View and Access Objects

#### 1️⃣ Object Details

1. **Click on your uploaded object** (e.g., `coffee.jpg`)
2. **Review object properties:**
   - Upload location and timestamp
   - File size and type
   - **Object URL** (important for next step)

#### 2️⃣ Test Object Access

**Method 1: S3 Console "Open"**
1. **Click "Open"** button in object details
2. **Result:** File opens and displays correctly
3. **Why it works:** Uses your AWS credentials automatically

**Method 2: Public Object URL**
1. **Copy the Object URL** from object details
2. **Open URL in new browser tab**
3. **Result:** `Access Denied` error
4. **Why it fails:** Object is private by default

#### 3️⃣ Understanding URL Types

**Pre-signed URL (from "Open" button):**
- **Contains:** Your credentials encoded in the URL
- **Access:** Works because S3 can verify your identity
- **Security:** Only you can use this URL
- **Format:** Very long URL with authentication parameters

**Public Object URL:**
- **Contains:** Just the basic S3 path
- **Access:** Fails because object is private
- **Security:** Would work if object was made public
- **Format:** Simple `https://bucket-name.s3.region.amazonaws.com/object-key`

> 💡 **Key Insight:** S3 objects are private by default. The console "Open" feature uses pre-signed URLs with your credentials.

---

### 📝 Step 4: Organize Objects with Folders

#### 1️⃣ Create a Folder

1. **Back in your bucket** → **Click "Create folder"**
2. **Folder name:** `images`
3. **Create folder**

> 💡 **Remember:** These aren't real directories - they're key prefixes that create the appearance of folders.

#### 2️⃣ Upload to Folder

1. **Click on the `images` folder** to enter it
2. **Upload a file** (e.g., `beach.jpg`)
3. **Verify destination:** Should show `your-bucket/images/`
4. **Complete upload**

#### 3️⃣ Navigate Folder Structure

1. **View uploaded file** in the `images` folder
2. **Navigate up one level** to see folder in bucket root
3. **Experience:** Similar to cloud storage services like Google Drive or Dropbox

---

### 📝 Step 5: Clean Up Resources

#### 1️⃣ Delete Folder and Contents

1. **Select the folder** you want to delete
2. **Click "Delete"**
3. **Confirmation:** Type `permanently delete` in the text input
4. **Delete objects**

> ⚠️ **Warning:** This permanently deletes the folder and all its contents.

---

### 🔍 Key Observations

**Global Bucket Naming:**
- Experienced firsthand that bucket names must be globally unique
- Learned naming strategies to avoid conflicts

**Security by Default:**
- Objects are private by default (Access Denied on public URLs)
- Pre-signed URLs provide secure access with your credentials

**Folder Illusion:**
- Folders look like traditional directories in the UI
- Actually implemented as key prefixes (no true directories)

**Regional vs Global View:**
- Buckets created in specific regions
- S3 console shows all buckets across all regions

---

## 🤝 S3 Shared Responsibility Model

### 📋 Overview

Understanding the **Shared Responsibility Model** for Amazon S3 is crucial for proper security and operational management. AWS and customers each have specific areas of responsibility to ensure S3 operates securely and effectively.

---

### 🏢 AWS Responsibilities

#### 🏗️ Infrastructure Management
- **Global infrastructure** – Data centers, networking, and physical security
- **S3 service availability** – Ensuring the service remains accessible and operational
- **Facility resilience** – Ability to sustain concurrent failures of multiple facilities
- **Hardware maintenance** – Managing underlying storage and compute infrastructure

#### 🔧 Internal Operations
- **Configuration management** – Internal AWS service configurations and settings
- **Vulnerability analysis** – Security scanning and patching of AWS infrastructure
- **Compliance validation** – AWS internal compliance with industry standards and regulations
- **Service updates** – Maintaining and updating the S3 service platform

#### 🛡️ Platform Security
- **Physical security** – Securing data centers and hardware
- **Network security** – Protecting AWS network infrastructure
- **Hypervisor security** – Securing virtualization layers
- **Service isolation** – Ensuring customer data separation

---

### 👤 Customer Responsibilities

#### 🔐 Security Configuration
- **S3 Bucket Policies** – Configuring proper access controls and permissions
- **IAM policies** – Setting up user and role-based access controls
- **Access Control Lists (ACLs)** – Managing object-level permissions
- **Public access settings** – Preventing unintended public exposure

#### 📦 Data Management
- **S3 Versioning** – Enabling and managing object versioning for data protection
- **Data replication** – Setting up cross-region or same-region replication
- **Backup strategies** – Implementing appropriate data backup and recovery plans
- **Data lifecycle** – Managing object transitions and expiration policies

#### 🔒 Encryption
- **Encryption at rest** – Choosing and configuring server-side encryption (SSE-S3, SSE-KMS, SSE-C)
- **Encryption in transit** – Using HTTPS for data transfer
- **Client-side encryption** – Implementing encryption before upload (optional)
- **Key management** – Managing encryption keys (especially for SSE-C and client-side encryption)

#### 📊 Monitoring and Optimization
- **Logging and monitoring** – Enabling CloudTrail, S3 server access logs, and CloudWatch
- **Cost optimization** – Choosing appropriate storage classes and lifecycle policies
- **Performance optimization** – Configuring request patterns and access patterns
- **Usage monitoring** – Tracking data access and transfer patterns

#### ⚡ Operational Excellence
- **Application integration** – Properly integrating applications with S3
- **Error handling** – Implementing retry logic and error handling in applications
- **Testing** – Validating backup, recovery, and access procedures
- **Documentation** – Maintaining records of configurations and procedures

---

### 📊 Responsibility Summary

| Area | AWS Responsibility | Customer Responsibility |
|------|-------------------|------------------------|
| **Infrastructure** | Physical security, data centers, networking | Application architecture, integration |
| **Platform** | S3 service availability, updates, patching | Bucket configuration, policies, access controls |
| **Data** | Infrastructure protection, facility resilience | Data classification, versioning, replication |
| **Encryption** | Encryption infrastructure (SSE-S3, SSE-KMS) | Encryption configuration, key management |
| **Access Control** | Platform access controls | Bucket policies, IAM policies, public access settings |
| **Monitoring** | Infrastructure monitoring | Application monitoring, logging, cost optimization |
| **Compliance** | Infrastructure compliance validation | Data compliance, regulatory requirements |

---

### 🎯 Key Distinctions

**AWS Focus:**
- **Infrastructure layer** – Everything below your data and configurations
- **Service reliability** – Keeping S3 available and performant
- **Security of the cloud** – Protecting the underlying platform

**Customer Focus:**
- **Configuration layer** – All settings and policies you control
- **Data protection** – Ensuring your data is secure and accessible
- **Security in the cloud** – Protecting your data and access patterns

> 💡 **Remember:** AWS secures the foundation, but customers must secure their implementation and data on top of that foundation.

---

## 🎯 Key Takeaways

- **S3 is fundamental** – One of the main building blocks of AWS and the web
- **Infinitely scalable** – Can store virtually unlimited amounts of data
- **Buckets are containers** – Top-level directories with globally unique names
- **Regional but global naming** – Buckets created in regions but names must be globally unique
- **Objects have keys** – Full path identifiers that may look like directory structures
- **No real directories** – Everything is stored as keys with forward slashes
- **Large file support** – Up to 5 TB per object with multi-part upload for files > 5 GB
- **Rich metadata** – Objects can have custom metadata, tags, and version IDs
- **Versatile use cases** – From backup and archival to big data analytics and web hosting

# 🔄 Amazon S3 Replication

## 📋 Overview

**Amazon S3 Replication** automatically replicates objects from one S3 bucket to another, providing data redundancy, compliance, and improved performance. S3 offers two types of replication to meet different needs: Cross-Region Replication (CRR) and Same-Region Replication (SRR).

---

## 🌐 Types of S3 Replication

### 🔄 Cross-Region Replication (CRR)

**CRR** replicates objects from a source bucket in one AWS region to a destination bucket in a **different** AWS region.

#### 🔑 Key Characteristics
- **Different regions** – Source and destination must be in different AWS regions
- **Global distribution** – Spread data across geographical locations
- **Disaster recovery** – Protect against regional failures
- **Compliance** – Meet regulatory requirements for data location

### 🔄 Same-Region Replication (SRR)

**SRR** replicates objects from a source bucket to a destination bucket within the **same** AWS region.

#### 🔑 Key Characteristics
- **Same region** – Both buckets in the same AWS region
- **Account separation** – Often used between different AWS accounts
- **Environment isolation** – Separate production and test data
- **Log aggregation** – Centralize logs from multiple sources

---

## ⚙️ How S3 Replication Works

### 🏗️ Replication Architecture

```
Source Bucket (Region A) → Asynchronous Replication → Destination Bucket (Region B)
```

#### 🔄 Replication Process

1. **Object uploaded** to source bucket
2. **S3 identifies** replication rule match
3. **Asynchronous copying** begins in background
4. **Object replicated** to destination bucket
5. **Replication status** tracked for monitoring

### ⚡ Asynchronous Nature

- **Background process** – Happens behind the scenes
- **Non-blocking** – Doesn't affect source bucket operations
- **Eventually consistent** – Objects appear in destination after some time
- **Automatic** – No manual intervention required

---

## 📋 Requirements

### ✅ Prerequisites

**1. Versioning Enabled**
- **Source bucket** – Versioning must be enabled
- **Destination bucket** – Versioning must be enabled
- **Required for both** CRR and SRR

**2. Region Requirements**
- **CRR** – Source and destination regions **must be different**
- **SRR** – Source and destination regions **must be the same**

**3. IAM Permissions**
- **S3 service role** – Must have permissions to read from source
- **Write permissions** – Must have permissions to write to destination
- **Proper IAM setup** – Service needs access to specified buckets

### 🔐 Cross-Account Support

- **Different AWS accounts** – Buckets can be in different accounts
- **Cross-account permissions** – Additional IAM setup required
- **Bucket policies** – May need destination bucket policies

---

## 🎯 Use Cases

### 🌍 Cross-Region Replication (CRR)

#### 📊 Compliance Requirements
- **Regulatory compliance** – Meet data residency requirements
- **Legal requirements** – Store data in specific geographical locations
- **Industry standards** – Comply with sector-specific regulations

#### ⚡ Lower Latency Access
- **Global users** – Serve data from regions closer to users
- **Performance improvement** – Reduce data access latency
- **Content distribution** – Distribute content worldwide

#### 🔄 Cross-Account Replication
- **Data sharing** – Share data between different AWS accounts
- **Organizational separation** – Keep data separate but accessible
- **Backup across accounts** – Additional layer of data protection

### 🏢 Same-Region Replication (SRR)

#### 📝 Log Aggregation
- **Centralized logging** – Aggregate logs from multiple S3 buckets
- **Analytics preparation** – Combine data for analysis
- **Compliance reporting** – Centralize audit trails

#### 🔄 Live Replication Between Environments
- **Production to test** – Keep test environment updated with production data
- **Development environments** – Provide realistic test data
- **Staging synchronization** – Keep staging in sync with production

---

## ⚙️ Configuration Requirements

### 📝 Replication Rules

**Rule Components:**
- **Source bucket** – Which bucket to replicate from
- **Destination bucket** – Where to replicate objects
- **Prefix/filter** – Which objects to replicate (optional)
- **Storage class** – Destination storage class (optional)

### 🔐 IAM Role Configuration

**Required permissions for S3 service:**
```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Action": [
                "s3:ListBucket",
                "s3:GetReplicationConfiguration",
                "s3:GetObjectVersionForReplication",
                "s3:GetObjectVersionAcl",
                "s3:GetObjectVersionTagging",
                "s3:GetObjectRetention",
                "s3:GetObjectLegalHold"
            ],
            "Effect": "Allow",
            "Resource": [
                "arn:aws:s3:::s3-bucket-origin-v1",
                "arn:aws:s3:::s3-bucket-origin-v1/*",
                "arn:aws:s3:::s3-bucket-replica-v1",
                "arn:aws:s3:::s3-bucket-replica-v1/*"
            ]
        },
        {
            "Action": [
                "s3:ReplicateObject",
                "s3:ReplicateDelete",
                "s3:ReplicateTags",
                "s3:ObjectOwnerOverrideToBucketOwner"
            ],
            "Effect": "Allow",
            "Resource": [
                "arn:aws:s3:::s3-bucket-origin-v1/*",
                "arn:aws:s3:::s3-bucket-replica-v1/*"
            ]
        }
    ]
}
```

---

## ⚠️ Important Considerations

### 🔄 What Gets Replicated

**Replicated:**
- **New objects** uploaded after replication is configured
- **Object metadata** and ACLs
- **Object tags** (if configured)

**Not Replicated:**
- **Existing objects** (uploaded before replication setup)
- **Objects created by lifecycle actions**
- **Objects in Glacier or Deep Archive** (unless restored)

### 💰 Cost Implications

- **Replication charges** – Pay for cross-region data transfer (CRR)
- **Storage costs** – Pay for storage in destination bucket
- **Request costs** – PUT requests for replicated objects

### 🔒 Security Considerations

- **Encryption** – Can replicate encrypted objects
- **Access controls** – Destination bucket may have different permissions
- **Cross-account** – Additional security setup required

---

## 📊 Summary

| Feature | CRR | SRR |
|---------|-----|-----|
| **Regions** | Different regions | Same region |
| **Use Cases** | Compliance, latency, DR | Log aggregation, test environments |
| **Data Transfer** | Cross-region (charged) | Within region (free) |
| **Compliance** | Meet geo-requirements | Environment separation |
| **Latency** | Improve global access | Same region performance |
| **Accounts** | Can be cross-account | Often cross-account |

---

## 🛠️ Hands-On: Setting Up S3 Cross-Region Replication

### 📋 Step 1: Create Source Bucket

1. **Navigate to S3 console** and click **"Create bucket"**
2. **Bucket name**: `s3-[your-name]-bucket-origin-v1` (must be globally unique)
3. **Region**: Select your preferred region (e.g., EU West 1 - Ireland)
4. **Bucket Versioning**: Enable **"Bucket Versioning"**
5. Leave other settings as default and click **"Create bucket"**

### 📋 Step 2: Create Destination Bucket

1. **Create a second bucket** with name: `s3-[your-name]-bucket-replica-v1`
2. **Region**: Choose a **different region** for CRR (e.g., US East 1 - N. Virginia)
   - *For SRR, choose the same region as source*
3. **Bucket Versioning**: Enable **"Bucket Versioning"**
4. Click **"Create bucket"**

### 📋 Step 3: Upload Initial File (Before Replication)

1. **Open the source bucket**
2. Click **"Upload"** → **"Add files"**
3. **Upload a test file** (e.g., `beach.jpg`)
4. Click **"Upload"**
5. **Note**: This file will NOT be replicated automatically

### 📋 Step 4: Configure Replication Rule

1. **In source bucket**, go to **"Management"** tab
2. Scroll down to **"Replication rules"** section
3. Click **"Create replication rule"**

#### ⚙️ Replication Rule Configuration

**Rule Details:**
- **Rule name**: `demo-replication-rule`
- **Status**: Enable
- **Rule scope**: Apply to all objects in the bucket

**Source:**
- Leave default settings (entire bucket)

**Destination:**
- **Destination bucket**: Select **"Buckets in this account"**
- **Bucket name**: Enter your destination bucket name
- **Destination region**: Verify it shows your chosen region

**IAM Role:**
- Select **"Create new role"** (AWS will create the necessary permissions)

4. **Additional settings**: Leave defaults for now
5. Click **"Save"**

### 📋 Step 5: Handle Existing Objects Prompt

When prompted about existing objects:
- **Choose**: "No, do not replicate existing objects"
- **Reason**: Replication only applies to new objects uploaded after setup
- **Note**: Existing objects would require S3 Batch Operations to replicate

### 📋 Step 6: Test Replication with New Upload

1. **Upload a new file** to the source bucket (e.g., `coffee.jpg`)
2. **Enable "Show versions"** to see version IDs
3. **Note the version ID** of the uploaded object

### 📋 Step 7: Verify Replication

1. **Switch to destination bucket**
2. **Refresh the page** (may take 5-10 seconds)
3. **Observe**: New file appears in destination bucket
4. **Enable "Show versions"** in destination bucket
5. **Verify**: Version ID matches the source bucket exactly

### 📋 Step 8: Test Replication of Existing File

1. **Re-upload the initial file** (e.g., upload `beach.jpg` again)
2. **Check source bucket**: New version created with different version ID
3. **Check destination bucket**: New version appears (the previous version that wasn't there)
4. **Verify**: Only the new version gets replicated

---

## 🔍 Hands-On Observations

### ✅ What You Should See

**Source Bucket:**
- Contains all uploaded files
- Shows all versions (including pre-replication uploads)
- Each object has a unique version ID

**Destination Bucket:**
- Contains only files uploaded AFTER replication was configured
- Version IDs match the source bucket exactly
- Replication typically takes 5-15 seconds

### ⚠️ Important Notes

- **Existing objects** are NOT replicated automatically
- **Only new uploads** trigger replication
- **Version IDs are preserved** during replication
- **Replication is asynchronous** – expect small delays
- **Cross-region replication** incurs data transfer charges

---

## 🎯 Key Takeaways

- **Two types** – CRR (Cross-Region) and SRR (Same-Region) replication
- **Versioning required** – Must be enabled on both source and destination buckets
- **Asynchronous process** – Replication happens in the background automatically
- **IAM permissions needed** – S3 service must have proper read/write permissions
- **Cross-account support** – Buckets can be in different AWS accounts
- **CRR use cases** – Compliance, lower latency, cross-account data sharing
- **SRR use cases** – Log aggregation, production-to-test environment sync
- **Cost awareness** – Consider data transfer and storage costs
- **Security integration** – Works with encryption and access controls

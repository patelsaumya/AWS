# 🔍 AWS CloudTrail

## 📋 Overview

**AWS CloudTrail** is a service that provides **governance, compliance, and audit** for your AWS account. It records a history of all API calls and events that happen within your account.

---

## ⚡ Key Characteristics

### **Enabled by Default**

- **Automatic activation** – CloudTrail is enabled by default for every AWS account
- **No setup required** – Starts logging immediately when account is created
- **Comprehensive logging** – Captures all API calls and events automatically

### **What Gets Logged**

CloudTrail logs **everything** that happens in your AWS account:

- **Console activity** – All actions performed through AWS Management Console
- **SDK calls** – API calls made using AWS SDKs
- **CLI commands** – Commands executed via AWS Command Line Interface
- **Service activity** – Actions performed by AWS services
- **IAM users and roles** – All API calls made by IAM users and roles

---

## 📥 Log Destinations

CloudTrail logs can be sent to:

### **1. CloudWatch Logs**

- **Real-time monitoring** – Monitor and react to events in real-time
- **Integration** – Use CloudWatch Logs Insights for analysis
- **Alarms** – Set up alarms based on CloudTrail events

### **2. Amazon S3**

- **Long-term retention** – Store logs indefinitely
- **Compliance** – Meet regulatory requirements for log retention
- **Analysis** – Use S3 with Athena or other analytics tools

### **3. CloudTrail Console**

- **View recent events** – Access event history directly in console
- **Quick inspection** – Review API calls and events without additional setup

---

## 🌍 Trail Configuration

### **Multi-Region vs Single Region**

When creating a CloudTrail trail, you can choose:

- **All regions** – Monitor events across all AWS regions
  - **Recommended** – Ensures comprehensive audit trail
  - **Global coverage** – Captures activity regardless of region
- **Single region** – Monitor events in one specific region only
  - **Cost optimization** – Lower storage costs
  - **Limited coverage** – May miss events in other regions

---

## 🎯 Use Cases

### **Audit and Compliance**

- **Track all changes** – See who made what changes and when
- **Compliance requirements** – Meet regulatory and audit requirements
- **Security investigations** – Investigate security incidents

### **Example Scenario**

**Question:** A user deleted something. How do we know:
- **What** was deleted?
- **Who** deleted it?
- **When** was it deleted?

**Answer:** **CloudTrail** – Review CloudTrail logs to find the deletion event with all details.

---

## 📊 What You Can See

From the CloudTrail console, you can view:

- **SDK usage** – All API calls made via SDKs
- **CLI usage** – All commands executed via CLI
- **Console activity** – All actions performed in the console
- **IAM users and roles** – All API calls made by IAM principals
- **API call history** – Complete audit trail of all API calls

---

## 🔄 How It Works

```
API Call/Event → CloudTrail → Log Destination
     ↓              ↓              ↓
(Console,      (Records      (CloudWatch
 SDK, CLI,     event)        Logs, S3)
 Service)
```

1. **Event occurs** – API call or event happens in AWS account
2. **CloudTrail captures** – Event is automatically logged by CloudTrail
3. **Log stored** – Event stored in CloudTrail console
4. **Optional forwarding** – Logs can be sent to CloudWatch Logs or S3 for long-term retention

---

## 🛠️ Hands-On

### **Step 1: View Event History**

1. Navigate to **CloudTrail** → **Event history**
2. **View management events:**
   - Shows last **90 days** of management events
   - All API calls made in your account are displayed
   - Events appear in chronological order

### **Step 2: Perform an Action and Verify in CloudTrail**

1. **Perform an action:**
   - Go to **EC2** console
   - Select an instance
   - **Terminate** the instance
2. **Wait a few minutes** – CloudTrail events may take a few minutes to appear
3. **Refresh CloudTrail event history**
4. **Find the event:**
   - Look for "TerminateInstances" API call
   - Event appears in the event history list

### **Step 3: View Event Details**

1. **Click on the event** to view details
2. **Event information includes:**
   - **Event name** – API call name (e.g., TerminateInstances)
   - **Event source** – Service that generated the event (e.g., EC2)
   - **Access key** – Access key used for the API call
   - **Region** – Region where the event occurred
   - **Time** – When the event occurred
   - **User identity** – Who made the API call
3. **View full event JSON:**
   - Click to see complete event details in JSON format
   - Contains all metadata about the API call

---

## 🎯 Key Takeaways

✅ **CloudTrail = Audit and Compliance** – Provides governance, compliance, and audit for AWS accounts

✅ **Enabled by default** – Automatically active for every AWS account

✅ **Logs everything:**
- Console activity
- SDK calls
- CLI commands
- Service activity
- IAM users and roles

✅ **Log destinations:**
- **CloudTrail Console** – View recent events
- **CloudWatch Logs** – Real-time monitoring and analysis
- **Amazon S3** – Long-term retention and compliance

✅ **Trail configuration:**
- **All regions** – Monitor all regions (recommended)
- **Single region** – Monitor one region only

✅ **Use cases:**
- Audit and compliance
- Security investigations
- Track who did what and when
- Answer: "Who deleted this resource?" → **CloudTrail**

✅ **Long-term retention** – Send logs to CloudWatch Logs or S3 for extended storage

✅ **Complete audit trail** – History of all API calls and events in your AWS account

---


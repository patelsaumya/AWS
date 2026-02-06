# 🎯 Amazon EventBridge

## 📋 Overview

**Amazon EventBridge** (formerly **CloudWatch Events**) is a serverless event bus service that allows you to react to events happening within your AWS account. It enables event-driven architectures by connecting event sources to targets.

⚠️ **Note:** If you see "CloudWatch Events" in documentation, it refers to **Amazon EventBridge** (the new name).

---

## 🎯 Use Cases

### **1. Scheduled Cron Jobs** - *Event Schedules*

- **Schedule events** – Create rules that trigger at regular intervals (e.g., every hour)
- **Serverless execution** – Trigger Lambda functions on schedule
- **Example:** Run a script every hour using EventBridge → Lambda

### **2. React to Service Events** - *Event Pattern*

- **Monitor AWS services** – React when services perform specific actions
- **Security alerts** – Example: Alert security team when root user signs in
- **Automation** – Trigger actions based on service state changes

---

## 📥 Event Sources

EventBridge can receive events from:

- **EC2 Instances** – Instance state changes, lifecycle events
- **CodeBuild** – Build status changes
- **S3 Events** – Object creation, deletion, etc.
- **Trusted Advisor** – Security and cost optimization findings
- **Schedules** – Cron-based or rate-based schedules
- **Many AWS services** – Most AWS services can send events to EventBridge

---

## 📤 Event Destinations

EventBridge can trigger:

- **Lambda functions** – Execute serverless functions
- **SNS topics** – Send notifications (email, SMS, etc.)
- **SQS queues** – Send messages to queues
- **Compute services** – EC2, ECS, Batch
- **Integration services** – Step Functions, API Gateway
- **Orchestration** – Various workflow and automation services

---

## 🚌 Event Buses

### **1. Default Event Bus**

- **AWS service events** – Events from AWS services within your account
- **Schedules** – Cron and rate-based scheduled events
- **Built-in** – Automatically available in every AWS account

### **2. Partner Event Bus**

- **Third-party integrations** – Events from AWS partners (Zendesk, Datadog, etc.)
- **External events** – React to events happening outside AWS
- **Partner ecosystem** – Integrate with SaaS applications

### **3. Custom Event Bus**

- **Custom applications** – Your own applications can send events
- **Custom integrations** – Build event-driven architectures
- **Full control** – Define your own event schemas and flows

---

## ⚡ Additional Capabilities

### **Schema Registry**

- **Event schemas** – Model and discover event schemas
- **Data types** – Understand event structure and data types
- **Documentation** – Auto-generate code bindings from schemas

### **Event Archiving and Replay**

- **Archive events** – Store events indefinitely or for a set period
- **Replay events** – Replay archived events to test or recover
- **Audit trail** – Maintain historical event records

---

## 🔄 How It Works

```
Event Source → EventBridge → Target
     ↓              ↓           ↓
  (EC2, S3,    (Event Bus)  (Lambda,
  Schedule,              SNS, SQS,
  etc.)                  etc.)
```

1. **Event occurs** – Source generates an event
2. **EventBridge receives** – Event is sent to an event bus
3. **Rule matches** – EventBridge rules evaluate the event
4. **Target triggered** – Matching rule triggers the configured target

---

## 🛠️ Hands-On

### **Step 1: Create EventBridge Schedule (Rate-Based)**

1. Navigate to **EventBridge** → **Schedules** → **Create schedule**
2. **Name:** InvokeLambdaFunctionEveryOneHour
3. **Schedule type:** Recurring schedule
4. **Schedule pattern:**
   - Choose **Rate-based schedule**
   - Enter: `rate(1 hour)` (or use cron expression if preferred)
5. **Target:**
   - **Templated target:** Invoke Lambda function
   - **Function:** Select your Lambda function (e.g., demo-lambda)
6. **Permissions:** EventBridge creates IAM role automatically
7. **Create schedule** – Lambda will now run every hour

### **Step 2: Create EventBridge Rule - Console Sign In Alert**

1. Navigate to **EventBridge** → **Rules** → **Create rule**
2. **Name:** DemoSignInAlert
3. **Event pattern:**
   - Use **Event builder** (new interface)
   - **Event source:** AWS Service Events
   - **Service:** Search for "Sign In"
   - **Event type:** AWS Console Sign In via CloudTrail
   - Drop event into pattern builder
4. **Target:**
   - **Target type:** SNS topic
   - **Topic:** Select your SNS topic (e.g., demo-ccp)
   - **Execution role:** EventBridge creates role automatically
5. **Event bus:** Default event bus
6. **Enable rule:** Yes
7. **Create rule** – Email notifications sent on console sign-ins

### **Step 3: Create EventBridge Rule - EC2 Instance Termination Alert**

1. Navigate to **EventBridge** → **Rules** → **Create rule**
2. **Name:** InstanceTerminatedNotification
3. **Event pattern:**
   - **Event source:** AWS Service Events
   - **Service:** EC2 Instance State-change Notification
   - **Event filter:** Add filter
     - **Field:** State
     - **Operator:** Equals
     - **Value:** terminated
4. **Target:**
   - **Target type:** SNS topic
   - **Topic:** Select your SNS topic
5. **Enable rule:** Yes
6. **Create rule** – Email notifications sent when EC2 instances are terminated

### **Testing**

- **Schedule:** Wait for scheduled time or check Lambda logs
- **Sign In Alert:** Sign in to AWS Console → Check email for notification
- **Termination Alert:** Terminate an EC2 instance → Check email for notification

---

## 🎯 Key Takeaways

✅ **EventBridge = CloudWatch Events** – Same service, new name

✅ **Purpose:** React to events happening within AWS accounts

✅ **Use Cases:**
- Scheduled cron jobs (serverless)
- React to service events (security alerts, automation)

✅ **Event Sources:**
- EC2, CodeBuild, S3 Events, Trusted Advisor, Schedules, many AWS services

✅ **Event Destinations:**
- Lambda, SNS, SQS, compute services, integration services

✅ **Event Buses:**
- **Default** – AWS service events and schedules
- **Partner** – Third-party SaaS events (Zendesk, Datadog, etc.)
- **Custom** – Your own application events

✅ **Additional Features:**
- Schema Registry – Model and discover event schemas
- Event Archiving – Store events indefinitely or for set period
- Event Replay – Replay archived events

✅ **Event-driven architecture** – Connect event sources to targets automatically

✅ **Serverless** – No infrastructure to manage, pay per event

---


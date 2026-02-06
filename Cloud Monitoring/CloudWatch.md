# 📊 Amazon CloudWatch

## 📋 Overview

**Amazon CloudWatch** is a monitoring and observability service that provides metrics, alarms, and dashboards for AWS services and applications. It helps you gain visibility into the performance and health of your cloud deployments.

---

## 📈 CloudWatch Metrics

### 🔍 What are Metrics?

**Metrics** are variables to monitor over time:
- **Time-series data** – Metrics have timestamps and values
- **Visualization** – Create CloudWatch dashboards to view multiple metrics at once
- **Every AWS service** – CloudWatch provides metrics for all AWS services

### 💰 Billing Metric

- **Location:** Only available in **us-east-1** region
- **Purpose:** Shows total estimated charges for your AWS account
- **Behavior:** Resets to zero at the end of each month
- **Use case:** Track spending across your entire account

### 🖥️ EC2 Metrics

Common EC2 instance metrics:

- **CPUUtilization** – How much the CPU is being used
  - High utilization = instance may be too busy → scale up or out
- **StatusCheck** – Verifies EC2 instance is functioning properly
- **NetworkIn/NetworkOut** – Network traffic in and out of the instance

⚠️ **Note:** RAM (memory) is **not** an available metric for EC2 instances.

#### ⏱️ Monitoring Frequency

- **Default:** Metrics every **5 minutes**
- **Detailed Monitoring:** Metrics every **1 minute** (more expensive)

### 💾 EBS Metrics

- **DiskReadOps/DiskWriteOps** – Number of read/write operations
- **DiskReadBytes/DiskWriteBytes** – Amount of data read/written

### 🪣 S3 Metrics

- **BucketSizeBytes** – Total size of objects in bucket
- **NumberOfObjects** – Count of objects in bucket
- **AllRequests** – Number of requests to S3 bucket

### 📊 Other Metrics

- **Service Limits** – Track usage of service APIs
- **Custom Metrics** – Push your own custom metrics if needed

---

## 🚨 CloudWatch Alarms

### 🔔 What are Alarms?

**Alarms** trigger notifications when metrics cross thresholds:
- **Monitor any metric** – Set thresholds for any CloudWatch metric
- **Automatic actions** – Trigger actions when alarm state changes
- **Multiple states** – OK, INSUFFICIENT_DATA, or ALARM

### ⚡ Alarm Actions

When an alarm is triggered, you can configure actions:

#### 1. **Auto Scaling Actions**
- **Increase/Decrease** – Modify Auto Scaling Group desired capacity
- **Automatic scaling** – Scale EC2 instances based on metrics

#### 2. **EC2 Actions**
- **Stop** – Stop an EC2 instance
- **Terminate** – Terminate an EC2 instance
- **Reboot** – Reboot an EC2 instance
- **Recover** – Recover an EC2 instance

#### 3. **SNS Notifications**
- **Send alerts** – Publish to SNS topic (email, SMS, etc.)
- **Example:** If CPU utilization > 90%, send email notification

### ⚙️ Alarm Configuration

- **Sampling options:** Average, Sum, Min, Max, Sample Count, Percentile
- **Evaluation period:** 5 minutes, 10 minutes, 1 hour, etc.
- **Data points:** Number of data points required to trigger alarm

### 💵 Billing Alarm

- **Monitor spending** – Create alarm on Billing metric
- **Set threshold** – Get notified when spending exceeds limit (e.g., $10, $20)
- **Prevent surprises** – Early warning for unexpected costs

### 📊 Alarm States

1. **OK** ✅ – Metric is within normal range (green)
2. **INSUFFICIENT_DATA** ⚠️ – Not enough data points to evaluate (yellow)
3. **ALARM** 🔴 – Metric has crossed threshold (red)

---

## 📝 CloudWatch Logs

### 🔍 What are Log Files?

**Log files** are text records written by applications:
- **Application activity** – Actions performed, user interactions, cleanup tasks
- **Troubleshooting** – Review logs to understand what the application did
- **Debugging** – Identify issues and track application behavior

### 📥 Log Sources

CloudWatch Logs can collect logs from:

- **Elastic Beanstalk** – Application logs from Beanstalk environments
- **ECS** – Container logs from ECS tasks
- **Lambda** – Function execution logs
- **CloudTrail** – API call logs
- **CloudWatch Logs Agent** – Installed on EC2 or on-premises servers
- **Route 53** – DNS query logs

### ⚡ Features

- **Real-time monitoring** – Monitor logs as they are generated
- **React to events** – Take action based on log content
- **Configurable retention** – Set retention periods:
  - 1 week, 30 days, 1 year, or **infinite** retention

### 🖥️ How It Works for EC2

**By default, EC2 instances do NOT send logs to CloudWatch Logs.**

To enable log collection:

1. **Install CloudWatch Logs Agent** – Agent runs on EC2 instance
2. **IAM Permissions** – EC2 instance must have IAM role with permissions to write to CloudWatch Logs
3. **Agent Configuration** – Configure which log files to send
4. **Log Flow:** EC2 Instance → CloudWatch Logs Agent → CloudWatch Logs Service

### 🏢 Hybrid Support

- **On-premises servers** – CloudWatch Logs Agent can be installed on on-premises servers
- **Unified collection** – Collect logs from both EC2 instances and on-premises servers
- **Single service** – All logs centralized in CloudWatch Logs

---

## 🛠️ Hands-On

### **Step 1: View Metrics**

1. Navigate to **CloudWatch** → **Metrics** → **All metrics**
2. Browse metrics by service:
   - **SQS Queue Metrics** – Messages received, deleted, sent
   - **EC2 Per-instance Metrics** – CPU utilization, status checks
   - Metrics appear after instances/services have been running

### **Step 2: Create Alarm from CloudWatch Console**

1. Go to **CloudWatch** → **Alarms** → **Create alarm**
2. **Select metric:** Choose EC2 CPU utilization for your instance
3. **Configure threshold:**
   - **Statistic:** Average
   - **Period:** 5 minutes
   - **Threshold:** Greater than 80%
4. **Add notification:** Create SNS topic → Add email subscription
5. **Name alarm:** DemoAlarm
6. **Create alarm** – Monitor threshold on dashboard

### **Step 3: Create Alarm from EC2 Console**

1. Go to **EC2** → Select instance → **Monitoring** tab
2. Click **+** next to **Alarm status**
3. **Recover instance alarm:**
   - **Metric:** Status check failed (system)
   - **Action:** Recover instance
   - **Notification:** SNS topic
4. **Reboot instance alarm:**
   - **Metric:** CPU utilization > 95% for 3 consecutive periods
   - **Action:** Reboot instance
   - **Use case:** Handle CPU stuck in loop

### **Step 4: Create Billing Alarm**

1. **Switch to us-east-1** (billing metrics only available here)
2. Go to **CloudWatch** → **Billing** → **Create alarm**
3. **Select metric:** EstimatedCharges (USD)
4. **Threshold:** Greater than $8 (or your limit)
5. **Notification:** Create SNS topic with email subscription
6. **Name:** DemoBillingAlarm
7. ⚠️ **Important:** Billing alarms only work in us-east-1 region

### **Step 5: Explore CloudWatch Logs**

1. Navigate to **CloudWatch** → **Logs** → **Log groups**
2. **View log groups:**
   - Log groups are automatically created by services (e.g., Lambda, ECS, Elastic Beanstalk)
   - Each service/application has its own log group
3. **Explore log streams:**
   - Click on a log group to view **log streams**
   - Each execution/instance creates a new log stream
   - Log streams contain chronological log entries
4. **View log entries:**
   - Each log entry shows timestamp, request ID, and log message
   - View application activity, errors, and debugging information
5. **Monitor in real-time:**
   - As services run, new log streams appear automatically
   - Log entries are added in real-time as applications execute
6. **Troubleshoot errors:**
   - Review log entries to identify exceptions and errors
   - Use log information to debug application issues
   - Track request IDs and execution flow

### **Key Observations**

- **Metrics dashboard** – View all service metrics in one place
- **Multiple alarm creation methods** – CloudWatch console or service-specific console (EC2)
- **Alarm actions** – SNS notifications, EC2 actions (recover, reboot), Auto Scaling
- **Billing alarm** – Must be created in us-east-1 region only
- **Alarm states** – Monitor OK, INSUFFICIENT_DATA, or ALARM states
- **CloudWatch Logs** – Log groups automatically created by services, real-time log monitoring, troubleshooting capabilities

---

## 🎯 Key Takeaways

✅ **CloudWatch Metrics** – Variables to monitor over time with timestamps

✅ **Billing Metric** – Only in us-east-1, shows total account charges, resets monthly

✅ **EC2 Metrics:**
- CPUUtilization, StatusCheck, NetworkIn/NetworkOut
- **No RAM metric** available
- Default: 5 minutes, Detailed: 1 minute (more expensive)

✅ **EBS Metrics** – Disk read/write operations and bytes

✅ **S3 Metrics** – Bucket size, object count, request count

✅ **Custom Metrics** – Push your own metrics if needed

✅ **CloudWatch Alarms** – Trigger notifications when metrics cross thresholds

✅ **Alarm Actions:**
- Auto Scaling (scale up/down)
- EC2 Actions (stop, terminate, reboot, recover)
- SNS Notifications (email, SMS alerts)

✅ **Alarm States:** OK (green), INSUFFICIENT_DATA (yellow), ALARM (red)

✅ **Billing Alarm** – Monitor spending and get notified when exceeding threshold

✅ **Dashboards** – Visualize multiple metrics together for better insights

✅ **CloudWatch Logs** – Collect and monitor log files from applications and services

✅ **Log Sources:**
- Elastic Beanstalk, ECS, Lambda, CloudTrail
- CloudWatch Logs Agent (EC2, on-premises)
- Route 53 DNS queries

✅ **CloudWatch Logs Agent:**
- **Required for EC2** – By default, EC2 instances don't send logs
- **Install agent** – Push log files to CloudWatch Logs
- **IAM permissions** – EC2 instance role needs CloudWatch Logs write permissions
- **Hybrid support** – Works on EC2 and on-premises servers

✅ **Log Features:**
- Real-time monitoring
- Configurable retention (1 week, 30 days, 1 year, infinite)
- React to log events

---


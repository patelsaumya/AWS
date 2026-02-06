# 🏥 AWS Health Dashboard

## 📋 Overview

**AWS Health Dashboard** provides visibility into the health of AWS services. It has **two parts**: Service History (general) and Your Accounts (account-specific).

---

## 📊 Two Components

### **1. Service History**

**Formerly:** AWS Service Health Dashboard

- **General service health** – Shows health status for all regions and services
- **Historical view** – Daily history of service behavior
- **RSS feed** – Subscribe to service health updates
- **Public information** – General status for all AWS customers

### **2. Health Dashboard for Your Accounts**

**Formerly:** AWS Personal Health Dashboard (PHD)

- **Account-specific health** – Events that impact **your account directly**
- **Personalized view** – Only shows services and resources you're actually using
- **Alerts and remediation** – Guidance when AWS experiences events affecting you
- **Proactive notifications** – Scheduled maintenance activities
- **Organization aggregation** – Aggregate data for entire AWS organization

---

## 🔍 Key Features

### **Service History**

- **All regions** – Health status across all AWS regions
- **All services** – Status of all AWS services
- **Daily history** – View past service health
- **RSS feed** – Subscribe for updates

### **Your Accounts Dashboard**

- **Direct impact** – Shows outages that directly impact you
- **Event log** – View past events that affected your account
- **Alerts** – Get notified about issues affecting your resources
- **Remediation guidance** – Steps to resolve issues
- **Scheduled activities** – Proactive notifications for maintenance
- **Performance and availability** – Monitor services you actually use

---

## 🚀 Access

- **Global service** – Available across all regions
- **No setup required** – Automatically available for your account

---

## 🛠️ Hands-On

### **Step 1: View Service History**

1. Click **Service History** tab
2. **View by region and day:**
   - Browse services by region (e.g., North America)
   - See daily health status for each service
   - Scroll to view all services
3. **Open issues:** Shows general service issues affecting all customers
4. **Filter:** Find specific service or region

### **Step 2: View Account Health**

1. **Open and Recent Issues:**
   - Shows issues impacting **your account**
   - Bell icon shows notification count when issues exist
2. **Schedule Changes:**
   - Proactive notifications for scheduled maintenance
   - Example: EBS volume maintenance
3. **Event Log:**
   - Past events that affected your account
   - Shows start time, last update, resolution status
   - Click event → View description, impact, affected resources

### **Step 3: Organization Health**

1. **Organization-wide visibility** – Configure to see health across all accounts
2. **Automation** – Integrate with EventBridge for automated responses

---

## 🎯 Key Takeaways

✅ **AWS Health Dashboard = Two parts:**
- **Service History** – General service health (all customers)
- **Your Accounts** – Account-specific health (personalized)

✅ **Service History:**
- Shows all regions and services health
- Historical view (daily)
- RSS feed available
- General/public information

✅ **Health Dashboard for Your Accounts:**
- Events that impact **you directly**
- Services and resources **you're using**
- Alerts, remediation guidance, proactive notifications
- Can aggregate for entire AWS organization
- Event log for past events

✅ **Access:** Top right corner (bell icon) in AWS Console

✅ **Use cases:**
- Monitor service health
- Get alerts for issues affecting your account
- View remediation guidance
- Track scheduled maintenance
- Review past events

---


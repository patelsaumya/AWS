# 🔄 Auto Scaling Groups (ASG)

## 📋 Overview

**Auto Scaling Groups (ASG)** automatically create and remove EC2 instances based on demand, ensuring your application can handle varying loads efficiently. ASGs work hand-in-hand with load balancers to provide elastic, cost-effective, and highly available infrastructure that adapts to real-world traffic patterns.

---

## 🔍 What is an Auto Scaling Group?

An **Auto Scaling Group** is a logical collection of EC2 instances that can automatically scale out (add instances) or scale in (remove instances) based on defined criteria. This enables your applications to handle changing demand patterns without manual intervention.

### 🌐 Real-World Example

Consider an e-commerce website:
- **During the day** → High shopping activity → Need more servers
- **During the night** → Low shopping activity → Need fewer servers
- **Holiday seasons** → Peak traffic → Maximum servers
- **Off-seasons** → Normal traffic → Standard server count

ASGs automatically adjust your infrastructure to match these patterns.

---

## 🎯 Why Use Auto Scaling Groups?

### ✅ Key Benefits

- **Scale Out** – Automatically add EC2 instances to match increased load
- **Scale In** – Automatically remove EC2 instances to match decreased load
- **Cost Optimization** – Only run the optimal number of instances at any time
- **High Availability** – Ensure minimum number of healthy instances are always running
- **Load Balancer Integration** – Automatically register/deregister instances with load balancers
- **Health Monitoring** – Replace unhealthy instances automatically
- **Elasticity** – Embody the core cloud principle of elastic infrastructure

### 💰 Cost Savings

ASGs provide **huge cost savings** by:
- Running only the capacity you need at any moment
- Automatically scaling in during low-demand periods
- Eliminating over-provisioning of resources
- Following the cloud principle of **pay-for-what-you-use**

---

## ⚙️ How Auto Scaling Groups Work

### 📊 Core Configuration

Every ASG has three key settings:

1. **Minimum Size** – The smallest number of instances that must always be running
2. **Desired Capacity** – The target number of instances (usually the current actual size)
3. **Maximum Size** – The largest number of instances the ASG can scale to

### 🔄 Scaling Process

#### Scaling Out (Adding Instances)
1. **Load increases** beyond threshold
2. **ASG detects** the increased demand
3. **New EC2 instances** are automatically launched
4. **Instances are registered** with the load balancer
5. **Traffic is distributed** across all healthy instances

#### Scaling In (Removing Instances)
1. **Load decreases** below threshold
2. **ASG detects** the reduced demand
3. **Excess EC2 instances** are automatically terminated
4. **Instances are deregistered** from the load balancer
5. **Traffic is redistributed** among remaining instances

---

## 🏗️ ASG and Load Balancer Integration

### 🤝 Working Together

ASGs and Load Balancers work **hand-in-hand** to provide seamless scaling:

```
Internet Traffic → Load Balancer → ASG Instances
                      ↓
               Automatic Registration
                      ↓
                 Health Monitoring
                      ↓
            Automatic Replacement/Scaling
```

### 📈 Scaling Example

**Initial State:**
- ASG: 1 EC2 instance (minimum size)
- Load Balancer: Routes traffic to 1 instance

**During High Load:**
- ASG: Scales to 5 EC2 instances
- Load Balancer: Automatically registers new instances and distributes traffic

**During Low Load:**
- ASG: Scales back to 2 EC2 instances
- Load Balancer: Automatically deregisters terminated instances

---

## 🏥 Health Monitoring and Self-Healing

### 🔍 Health Detection

ASGs continuously monitor instance health through:
- **EC2 Status Checks** – Instance and system status
- **ELB Health Checks** – Application-level health monitoring
- **Custom Health Checks** – Your own health verification logic

### 🔄 Automatic Recovery

When an **unhealthy instance** is detected:
1. **ASG identifies** the unhealthy instance
2. **Instance is terminated** and deregistered from load balancer
3. **New healthy instance** is launched automatically
4. **New instance is registered** with load balancer
5. **Service continues** without interruption

> 💡 **Example:** If there's an application bug causing an instance to fail, the ASG automatically replaces it with a fresh, healthy instance.

---

## 📐 ASG Configuration Settings

### 🔢 Size Settings

| Setting | Description | Example |
|---------|-------------|---------|
| **Minimum Size** | Always maintain at least this many instances | 1 |
| **Desired Capacity** | Target number of instances to run | 3 |
| **Maximum Size** | Never exceed this many instances | 10 |

### 🎯 Scaling Policies

- **Target Tracking** – Maintain a specific metric (e.g., CPU at 50%)
- **Step Scaling** – Scale based on metric thresholds
- **Simple Scaling** – Basic scale out/in based on alarms
- **Predictive Scaling** – Use machine learning to anticipate demand

### ⏰ Scaling Triggers

Common triggers for scaling actions:
- **CPU Utilization** – Scale when CPU usage is high/low
- **Memory Utilization** – Scale based on memory consumption
- **Request Count** – Scale based on number of requests
- **Custom Metrics** – Scale based on application-specific metrics

---

## 🌐 Multi-AZ Deployment

### 🏗️ High Availability Architecture

ASGs can deploy instances across multiple Availability Zones:
- **AZ-A:** 2 instances
- **AZ-B:** 2 instances  
- **AZ-C:** 1 instance

**Benefits:**
- **Fault tolerance** – Survive AZ failures
- **Load distribution** – Spread load geographically
- **Better performance** – Serve users from nearest AZ

---

## ✅ Best Practices

1. **Set appropriate scaling thresholds** – Avoid unnecessary scaling events
2. **Use multiple AZs** – Ensure high availability across zones
3. **Configure health checks** – Enable proper health monitoring
4. **Test scaling policies** – Verify scaling behavior before production
5. **Monitor costs** – Track scaling costs and optimize policies
6. **Use launch templates** – Define consistent instance configurations
7. **Implement warm-up periods** – Allow time for instances to initialize
8. **Set up notifications** – Get alerts for scaling events

---

## 📊 Summary

| Concept | Description |
|---------|-------------|
| **Purpose** | Automatically adjust EC2 instance count based on demand |
| **Scaling Out** | Add instances during high load |
| **Scaling In** | Remove instances during low load |
| **Size Settings** | Minimum, Desired, Maximum instance counts |
| **Health Monitoring** | Automatically replace unhealthy instances |
| **LB Integration** | Automatic registration/deregistration with load balancers |
| **Cost Benefits** | Run only optimal capacity, significant cost savings |
| **High Availability** | Multi-AZ deployment for fault tolerance |

---

## 📈 Auto Scaling Strategies

### 📋 Overview

Auto Scaling Groups support multiple scaling strategies to handle different use cases and traffic patterns. Understanding these strategies is crucial for designing efficient, cost-effective, and responsive applications.

---

### 🔧 Manual Scaling

**Manual Scaling** involves updating the size of an Auto Scaling Group manually through the AWS console, CLI, or API.

#### 🔑 Key Characteristics

- **Direct control** – You manually adjust the desired capacity
- **Immediate effect** – Changes take effect right away
- **Simple implementation** – No complex policies or triggers required

#### 🎯 Use Cases

- **Testing and development** – Fine-tune capacity during testing
- **One-time events** – Handle known traffic spikes manually
- **Emergency situations** – Quick response to unexpected issues
- **Cost optimization** – Manually scale in during maintenance windows

#### 📝 Example

- Change desired capacity from 1 to 2 instances
- Scale back from 2 to 1 instances when load decreases
- Temporarily scale to 5 instances for a marketing campaign

---

### ⚡ Dynamic Scaling

**Dynamic Scaling** automatically responds to changing demand based on real-time metrics and predefined policies.

#### 🔄 Simple/Step Scaling

**Simple and Step Scaling** use CloudWatch alarms to trigger scaling actions based on metric thresholds.

##### 🔑 How It Works

1. **Define CloudWatch alarms** based on metrics (CPU, memory, requests, etc.)
2. **Set scaling actions** for when alarms are triggered
3. **ASG responds automatically** by adding or removing instances

##### 📊 Example Policies

**Scale Out Policy:**
- **Trigger:** Average CPU utilization > 70% for 5 minutes
- **Action:** Add 2 instances to ASG capacity

**Scale In Policy:**
- **Trigger:** Average CPU utilization < 30% for 10 minutes  
- **Action:** Remove 1 instance from ASG capacity

---

#### 🎯 Target Tracking Scaling

**Target Tracking Scaling** is the easiest way to set up dynamic scaling by maintaining a specific target value for a metric.

##### 🔑 How It Works

1. **Choose a target metric** (e.g., average CPU utilization)
2. **Set a target value** (e.g., 40%)
3. **ASG automatically scales** to maintain that target

##### 📊 Example Configuration

- **Metric:** Average CPU Utilization
- **Target Value:** 40%
- **Result:** ASG automatically adds/removes instances to keep average CPU around 40%

##### ✅ Benefits

- **Simple setup** – Just define target metric and value
- **Automatic optimization** – ASG handles all scaling decisions
- **Responsive** – Continuously adjusts to maintain target
- **Built-in intelligence** – AWS algorithms optimize scaling timing

---

### 📅 Scheduled Scaling

**Scheduled Scaling** anticipates scaling needs based on known usage patterns and schedules scaling actions in advance.

#### 🔑 Key Characteristics

- **Proactive scaling** – Scale before demand hits
- **Time-based triggers** – Based on specific dates/times
- **Predictable patterns** – Handle known traffic patterns
- **Cost efficient** – Avoid reactive scaling delays

#### 🎯 Use Cases

- **Business hours scaling** – Scale out during work hours, scale in at night
- **Weekly patterns** – Higher capacity on weekdays, lower on weekends  
- **Seasonal events** – Black Friday, holiday shopping seasons
- **Sporting events** – Scale out before major games for betting/streaming apps
- **Batch processing** – Scale out for scheduled data processing jobs

#### 📝 Example Scenarios

**Sports Betting Example:**
- **Schedule:** Every Friday at 5:00 PM
- **Action:** Increase minimum capacity to 10 instances
- **Reason:** Anticipate traffic spike before weekend soccer games

**Business Hours Scaling:**
- **Morning:** 8:00 AM - Scale to 5 instances (work starts)
- **Evening:** 6:00 PM - Scale to 2 instances (work ends)
- **Night:** 11:00 PM - Scale to 1 instance (minimal activity)

---

### 🤖 Predictive Scaling

**Predictive Scaling** uses machine learning to analyze historical traffic patterns and automatically provision the right number of instances in advance.

#### 🔑 How It Works

1. **Machine learning algorithms** analyze past traffic patterns
2. **Forecast future demand** based on historical data
3. **Automatically provision instances** before predicted load increases
4. **Continuously learn** and improve predictions over time

#### 📊 Pattern Recognition

Predictive Scaling can identify and respond to patterns such as:
- **Daily cycles** – Traffic peaks for 3 hours every day
- **Weekly patterns** – Higher load on weekdays vs weekends
- **Monthly trends** – End-of-month processing spikes
- **Seasonal variations** – Holiday traffic increases

#### 🎯 Benefits

- **Proactive scaling** – Scale before demand hits (no lag time)
- **No manual intervention** – Fully automated ML-powered scaling
- **Cost optimization** – Right-size capacity based on actual patterns
- **Improved performance** – Instances ready when load increases
- **Continuous improvement** – ML models get better over time

#### 📈 Example Use Case

**E-commerce Website:**
- **Pattern:** Traffic consistently peaks from 7-10 PM daily
- **Predictive Action:** Automatically scale from 3 to 8 instances at 6:50 PM
- **Result:** Instances are ready before traffic spike hits
- **Benefit:** No performance degradation during peak hours

#### ⚠️ Important Notes

- **Requires historical data** – Needs consistent traffic patterns to learn from
- **Best for predictable workloads** – Most effective with recurring patterns
- **Exam focus** – Frequently appears in certification exams

---

## 📊 Scaling Strategies Comparison

| Strategy | Trigger | Response Time | Use Case | Complexity |
|----------|---------|---------------|----------|------------|
| **Manual** | Human intervention | Immediate | Testing, one-time events | Low |
| **Simple/Step** | CloudWatch alarms | Minutes | Reactive scaling | Medium |
| **Target Tracking** | Metric targets | Minutes | Maintain performance levels | Low |
| **Scheduled** | Time/date | Proactive | Known patterns | Medium |
| **Predictive** | ML predictions | Proactive | Recurring patterns | Low (setup) |

---

## 🎯 Choosing the Right Strategy

### 🔄 Reactive vs Proactive

**Reactive Strategies:**
- Simple/Step Scaling
- Target Tracking Scaling
- Response after load changes

**Proactive Strategies:**
- Scheduled Scaling  
- Predictive Scaling
- Scale before load changes

### 💡 Best Practices

1. **Combine strategies** – Use multiple scaling policies together
2. **Start simple** – Begin with Target Tracking, add complexity as needed
3. **Monitor and adjust** – Regularly review scaling performance
4. **Consider cost** – Balance performance needs with cost optimization
5. **Test thoroughly** – Validate scaling behavior before production

---

## 🧪 Hands-On: Creating an Auto Scaling Group

### 📋 Overview

Creating an Auto Scaling Group with Load Balancer integration to demonstrate automatic scaling and self-healing capabilities.

---

### 📝 Step 1: Create Launch Template

#### 1️⃣ Navigate to Launch Templates

1. **EC2 Console** → **Launch Templates** → **Create launch template**

#### 2️⃣ Configure Launch Template

1. **Launch template name:** `DemoLaunchTemplate`
2. **Template description:** `Template for ASG demo`

#### 3️⃣ Application and OS Images

1. **Quick Start** → **Amazon Linux**
2. **Select:** Amazon Linux 2 AMI

#### 4️⃣ Instance Configuration

1. **Instance type:** `t2.micro`
2. **Key pair:** `Don't include in launch template` (or select existing key pair)

#### 5️⃣ Network Settings

1. **Subnet:** `Don't include in launch template` (ASG will handle this)
2. **Security groups:** Select existing `launch-wizard-1` security group

#### 6️⃣ Storage Settings

- **Keep default settings** (8 GiB gp2)

#### 7️⃣ Advanced Details

**Scroll down to User Data** and add:

```bash
#!/bin/bash
yum update -y
yum install -y httpd
systemctl start httpd
systemctl enable httpd
echo "<h1>Hello World from $(hostname -f)</h1>" > /var/www/html/index.html
```

#### 8️⃣ Create Launch Template

1. **Review settings**
2. **Create launch template**

> ✅ **Expected Result:** Launch template successfully created and available for ASG use.

---

### 📝 Step 2: Create Auto Scaling Group

#### 1️⃣ Navigate to ASG

1. **EC2 Console** → **Auto Scaling Groups** → **Create Auto Scaling Group**

#### 2️⃣ Choose Launch Template

1. **Auto Scaling group name:** `DemoASG`
2. **Launch template:** Select `DemoLaunchTemplate` (Version 1)
3. **Next**

#### 3️⃣ Instance Type Requirements

1. **Keep default settings** from launch template (`t2.micro`)
2. **Next**

#### 4️⃣ Network Configuration

1. **VPC:** Select default VPC
2. **Availability Zones and subnets:** Select **3 availability zones**
3. **AZ rebalancing:** `Use balanced best effort distribution`
4. **Next**

---

### 📝 Step 3: Configure Load Balancing

#### 1️⃣ Attach to Load Balancer

1. **Load balancing:** Select `Attach to an existing load balancer`
2. **Choose from your load balancer target groups:** `demo-tg-alb`

> 📚 **Note:** This assumes you have the target group from the ELB hands-on lab. If not, create an ALB first.

#### 2️⃣ Health Checks

1. **EC2 health checks:** Enabled (default)
2. **ELB health checks:** **Enable** ✅
3. **Health check grace period:** 300 seconds (default)

> 💡 **Why ELB Health Checks:** If the load balancer detects unhealthy instances, ASG will automatically replace them.

#### 3️⃣ Additional Settings

1. **VPC Lattice:** No changes
2. **Zonal shift:** No changes
3. **Next**

---

### 📝 Step 4: Configure Group Size

#### 1️⃣ Group Size Settings

1. **Desired capacity:** `2`
2. **Minimum capacity:** `1`
3. **Maximum capacity:** `4`

#### 2️⃣ Scaling Policies

1. **For this demo:** Select `None` (no automatic scaling policies)
2. **Instance maintenance policy:** `No policy`

#### 3️⃣ Additional Capacity Settings

- **Keep default settings**

#### 4️⃣ Complete Creation

1. **Skip notifications and tags**
2. **Review and create**
3. **Create Auto Scaling Group**

---

### 📝 Step 5: Observe ASG in Action

#### 1️⃣ Monitor ASG Activity

1. **Go to your ASG** → **Activity tab**
2. **Observe:** Two activities showing instances being launched
3. **Instance management tab:** Two instances in "Pending" state

#### 2️⃣ Verify EC2 Instances

1. **EC2 Console** → **Instances**
2. **Verify:** Two new instances launched by ASG

#### 3️⃣ Check Load Balancer Integration

1. **Target Groups** → **demo-tg-alb** → **Targets tab**
2. **Verify:** Two targets registered (initially "Unhealthy")

#### 4️⃣ Speed Up Health Checks (Optional)

To make health checks faster for demo purposes:
1. **Target group** → **Health checks** → **Edit**
2. **Advanced settings:**
   - **Healthy threshold:** `2`
   - **Interval:** `5 seconds`
   - **Timeout:** `2 seconds`
3. **Save changes**

#### 5️⃣ Test Load Balancer

1. **Load Balancers** → **Your ALB** → **Copy DNS name**
2. **Open in browser** → Should see "Hello World"
3. **Refresh multiple times** → Should see different instance names

> ✅ **Expected Result:** Traffic balanced between two ASG-managed instances.

---

### 📝 Step 6: Test Self-Healing

#### 1️⃣ Terminate an Instance

1. **EC2 Console** → **Instances**
2. **Select one ASG instance**
3. **Instance State** → **Terminate instance**

#### 2️⃣ Observe ASG Response

1. **Go to ASG** → **Activity tab**
2. **Refresh page** and observe:
   - **Activity 1:** "Terminating EC2 instance"
   - **Activity 2:** "Launching a new EC2 instance in response to an unhealthy instance"

#### 3️⃣ Monitor Instance States

**Instance management tab:**
- **1 instance:** Pending (new replacement)
- **1 instance:** Terminating (being removed)
- **1 instance:** In Service (healthy existing instance)

#### 4️⃣ Verify Load Balancer

1. **Check target group** → Should maintain healthy targets
2. **Test ALB DNS** → Should continue to work normally

> ✅ **Expected Result:** ASG automatically replaces terminated instance, maintaining desired capacity of 2.

---

### 📝 Step 7: Test Manual Scaling (Optional)

#### 1️⃣ Change Desired Capacity

1. **ASG Details** → **Edit**
2. **Change desired capacity to:** `1`
3. **Save**
4. **Observe:** ASG terminates excess instance

#### 2️⃣ Scale Out

1. **Change desired capacity to:** `4`
2. **Save**
3. **Observe:** ASG launches 2 additional instances

> ✅ **Expected Result:** Load balancer automatically distributes traffic among all 4 instances.

---

## 🎯 Key Takeaways

- **ASGs provide elasticity** – automatically scale infrastructure up and down based on demand
- **Perfect for real-world patterns** – handle day/night cycles, seasonal variations, and traffic spikes
- **Cost optimization** – only pay for what you need when you need it
- **Self-healing** – automatically replace failed instances with healthy ones
- **Seamless LB integration** – instances are automatically registered/deregistered from load balancers
- **High availability** – deploy across multiple AZs for fault tolerance
- **Three key settings** – minimum size, desired capacity, maximum size
- **Multiple scaling triggers** – CPU, memory, request count, custom metrics
- **Embodies cloud elasticity** – core principle of cloud computing cost efficiency

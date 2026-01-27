# ⚡ AWS Lambda Overview

## 📋 Overview

**AWS Lambda** is a serverless compute service that lets you run code without provisioning or managing servers. You just upload your code as functions, and Lambda runs them on demand, automatically scaling based on the number of requests.

---

## 🔍 What is Lambda?

**AWS Lambda** is a Function as a Service (FaaS) that allows you to run functions in the cloud. Functions are limited by time (intended for shorter executions) and run on demand - you only pay when your code is running.

### 🔑 Key Characteristics

- **Serverless functions** – No servers to provision or manage
- **Time-limited** – Intended for shorter executions
- **On-demand** – Runs only when invoked
- **Automatic scaling** – Scales automatically as part of the service
- **Event-driven** – Functions invoked by events
- **Pay per use** – Pay only when functions run

---

## 🆚 Lambda vs EC2

### 📊 Comparison

| Feature | EC2 | Lambda |
|---------|-----|--------|
| **Type** | Virtual server | Virtual function |
| **Resources** | Fixed memory/CPU | Up to 10GB RAM (CPU scales with RAM) |
| **Runtime** | Continuously running | On-demand only |
| **Scaling** | Auto Scaling Group (slower) | Automatic (instant) |
| **Cost** | Pay for running time | Pay per request + compute time |
| **Use Case** | Long-running applications | Short, event-driven functions |

---

## 💰 Pricing Model

### 📊 Lambda Pricing

**Two Components:**
1. **Pay per request** – First 1 million requests free, then $0.20 per 1 million requests
2. **Pay per duration** – Based on compute time (GB-seconds)
> Gigabyte-seconds (GB-s or GBs) is a cloud computing billing metric, notably used by AWS Lambda, that measures total resource consumption by multiplying allocated memory (in GB) by execution time (in seconds)

**Free Tier:**
- **1 million invocations** per month (free)
- **400,000 GB-seconds** of compute time per month (free)
  - 400,000 seconds with 1GB RAM
  - 3.2 million seconds with 128MB RAM

**After Free Tier:**
- **$0.20** per 1 million requests
- **$1.00** per 600,000 GB-seconds

---

## 🔗 AWS Integration

### 📊 Event-Driven Service

**Lambda is event-driven:**
- **Reactive** – Functions invoked when events happen
- **AWS service integration** – Integrated with many AWS services
- **Automatic triggers** – Services automatically trigger Lambda functions
- **No polling** – Event-driven, not polling-based

**Common Integrations:**
- **S3** – Trigger on object uploads
- **DynamoDB** – Trigger on table changes
- **API Gateway** – Trigger on HTTP requests
- **EventBridge** – Trigger on scheduled events
- **Many more** – Integrated with entire AWS suite

---

## 💻 Supported Languages

### 📊 Programming Languages

**Native Support:**
- **Node.js/JavaScript** – Most popular
- **Python** – Very popular
- **Java**
- **C# (.NET Core)**
- **PowerShell**
- **Ruby**

**Custom Runtime API:**
- **Rust**
- **Go (Golang)**
- **Other languages** – Via Custom Runtime API

**Containers:**
- **Container images** – Lambda supports container images
- **Lambda Runtime API required** – Container images must implement the Lambda Runtime API
- **Note:** For Docker containers, prefer **ECS or Fargate** over Lambda

---

## 🎯 Use Cases

### 📊 Serverless Thumbnail Creation

**Example Architecture:**
```
User uploads image → S3 Bucket → Triggers Lambda → Creates thumbnail
                                              ↓
                                    Store in S3 + DynamoDB
```

**Process:**
1. **User uploads image** to S3 bucket
2. **S3 triggers Lambda** function automatically
3. **Lambda processes image** – Creates thumbnail
4. **Store results** – Thumbnail in S3, metadata in DynamoDB

**Benefits:**
- **Fully serverless** – S3, Lambda, DynamoDB (no servers)
- **Event-driven** – Automatic trigger on upload
- **Auto-scaling** – Handles any number of uploads

### ⏰ Serverless CRON Jobs

**Example Architecture:**
```
EventBridge (Schedule) → Triggers Lambda → Runs script
```

**Process:**
1. **EventBridge** (CloudWatch Events) triggers on schedule
2. **Lambda function** runs script automatically
3. **No servers** – Fully serverless CRON job

**Use Cases:**
- **Scheduled tasks** – Run every hour, day, week
- **Automated scripts** – No EC2 instance needed
- **Serverless automation** – EventBridge + Lambda

---

## ⚡ Key Features

### 📊 Lambda Capabilities

- **Easy monitoring** – CloudWatch integration
- **Resource allocation** – Up to 10GB RAM per function
- **CPU scaling** – CPU and network improve with RAM
- **Automatic scaling** – Handles any number of requests
- **Event-driven** – Reactive, triggered by events

---

## 🛠️ Hands-On: Creating Your First Lambda Function

### 📋 Step 1: Explore Lambda Console

1. **Navigate to Lambda Console** – Go to AWS Lambda service
2. **Try the Demo** – Visit `/begin` in the Lambda console URL to see an interactive demo
   - Shows how Lambda works with different languages (.NET, Java, Node.js, Python, Ruby)
   - Demonstrates event-driven scaling
   - Visualizes automatic scaling as events increase

### 📋 Step 2: Create a Lambda Function

1. **Click "Create a Function"**
2. **Choose Blueprint** – Select "Hello World" blueprint
3. **Configure Function:**
   - **Runtime:** Choose Python (or your preferred language)
   - **Function Name:** `HelloWorld`
   - **Execution Role:** Create a new role with basic Lambda permissions
     - This role allows Lambda to write logs to CloudWatch
4. **Review and Create** – Click "Create function"

### 📋 Step 3: Understand the Function Code

**Function Structure:**
- **Handler** – The function that gets invoked when an event is passed
- **Event Parameter** – Receives JSON data from the trigger
- **Return Value** – Returns a response

**Example Code (Python):**
```python
def lambda_handler(event, context):
    # Process the event
    value1 = event['key1']
    value2 = event['key2']
    value3 = event['key3']
    
    # Return response
    return value1
```

### 📋 Step 4: Test Your Function

1. **Click "Test" Button**
2. **Configure Test Event:**
   - Use the default "Hello World" template
   - JSON input example:
     ```json
     {
       "key1": "value1",
       "key2": "value2",
       "key3": "value3"
     }
     ```
3. **Save Test Event** – Name it (e.g., "HelloWorld") for reuse
4. **Run Test** – Click "Test" to execute
5. **View Results:**
   - **Execution Result** – Shows the returned value
   - **Logs** – Shows execution details
   - **Success/Failure** – Indicates if function executed successfully

### 📋 Step 5: Monitor Your Function

1. **View Metrics:**
   - Go to **Monitoring** tab
   - View invocations, duration, errors, throttles
   - Metrics populate after some time
2. **View CloudWatch Logs:**
   - Click **"View CloudWatch Logs"**
   - See detailed execution logs
   - Debug errors and trace execution flow
3. **Log Streams:**
   - Each execution creates a log entry
   - Shows input values, output, and any errors

### 📋 Step 6: Configure Your Function

1. **Go to Configuration Tab**
2. **General Configuration:**
   - **Memory** – Set from 128MB to 10GB (CPU scales with RAM)
   - **Ephemeral Storage** – Temporary storage for function
   - **Timeout** – Maximum execution time (default: 3 seconds, max: 15 minutes)
   - **Execution Role** – IAM role for Lambda permissions
3. **Permissions:**
   - **Role Summary** – View what the role allows
   - **CloudWatch Logs** – Allows writing logs
   - **Add Permissions** – Add S3, DynamoDB, etc., as needed

### 📋 Step 7: Add Triggers

1. **Go to Configuration → Triggers**
2. **Add Trigger:**
   - Click **"Add trigger"**
   - Choose from many event sources:
     - **S3** – Trigger on object uploads
     - **DynamoDB** – Trigger on table changes
     - **API Gateway** – Trigger on HTTP requests
     - **EventBridge** – Trigger on scheduled events
     - **Many more** – AWS and partner event sources
3. **Configure Trigger:**
   - For S3: Select bucket and event types
   - Configure trigger-specific settings

### 📋 Step 8: Understanding Execution Role

**Default Role Permissions:**
- **CloudWatch Logs** – Write logs to CloudWatch
- **Basic Lambda Permissions** – Execute function

**To Add More Permissions:**
1. Go to **Configuration → Permissions**
2. Click on the **Execution Role**
3. Add policies for:
   - **S3** – Read/write objects
   - **DynamoDB** – Read/write items
   - **Other AWS Services** – As needed

### 📋 Key Observations

- **Automatic Scaling** – Lambda scales automatically with events
- **Event-Driven** – Functions only run when triggered
- **Pay Per Use** – Only charged when function executes
- **Easy Debugging** – CloudWatch Logs show execution details
- **Flexible Configuration** – Adjust memory, timeout, and permissions

---

## 📊 Summary

| Feature | Description |
|---------|-------------|
| **Service Type** | Serverless Function as a Service (FaaS) |
| **Execution** | On-demand, time-limited |
| **Scaling** | Automatic |
| **Pricing** | Pay per request + compute time (duration) |
| **Free Tier** | 1M invocations, 400K GB-seconds |
| **Languages** | Node.js, Python, Java, C#, Ruby, and more |
| **Integration** | Event-driven, integrated with AWS services |
| **Use Cases** | Event processing, CRON jobs, serverless apps |

---

## 🎯 Key Takeaways

- **Lambda is serverless functions** – No servers, just functions
- **Run on demand** – Only runs when invoked, pay only when used
- **Time-limited** – Intended for shorter executions
- **Automatic scaling** – Scales automatically with requests
- **Event-driven** – Reactive service, triggered by events
- **Pricing model** – Pay per request (calls) and compute time (duration)
- **Free tier** – 1 million invocations, 400,000 GB-seconds per month
- **Multiple languages** – Node.js, Python, Java, C#, Ruby, and more
- **AWS integration** – Integrated with many AWS services
- **Use cases** – Thumbnail creation, CRON jobs, event processing
- **For containers** – Prefer ECS/Fargate over Lambda for Docker containers

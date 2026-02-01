# 📬 Amazon SQS (Simple Queue Service)

## 📋 Overview

**Amazon SQS** is a fully managed, serverless queue service that enables decoupling between applications. It allows producers to send messages to a queue, and consumers to poll and process those messages independently.

---

## 🔄 How SQS Works

### **Queue Model**
- **Producers** → Send messages into the queue (one or multiple)
- **Queue** → Stores messages temporarily
- **Consumers** → Poll the queue to retrieve messages (one or multiple)
- **Processing** → Consumers process messages and delete them when done

### **Message Flow**
1. Producer sends message → Queue stores it
2. Consumer polls queue → Retrieves message
3. Consumer processes message → Deletes from queue
4. Work is shared among consumers (horizontal scaling)

---

## ✨ Key Characteristics

### **Service Details**
- **AWS's oldest service** – Over 10 years old, one of the first AWS offerings
- **Fully managed & serverless** – No servers to provision or manage
- **Decoupling** – Applications communicate through the queue without direct dependencies

### **Performance & Scaling**
- **Seamless scaling** – From 1 message/second to tens of thousands per second
- **Low latency** – Less than 10 milliseconds for publish and subscribe
- **Horizontal scaling** – Consumers share work and scale independently
- **Unlimited messages** – No limit to messages in a queue

### **Message Retention**
- **Default retention:** 4 days
- **Maximum retention:** 14 days
- Messages must be processed within retention period

---

## 🏗️ Use Case: Decoupling Application Tiers

### **Architecture Example**
```
Web Servers (EC2 + ASG) 
    ↓ (sends messages)
SQS Queue
    ↓ (polls messages)
Video Processing (EC2 + ASG)
```

### **Benefits**
- **Independent scaling** – Web tier and processing tier scale separately
- **Auto-scaling based on queue depth** – Processing layer scales with message volume
- **Better user experience** – Web servers respond quickly, processing happens asynchronously
- **Cost efficiency** – Scale only what's needed, when needed

---

## 🔢 FIFO Queues

### **First In, First Out (FIFO)**
- **Ordering:** Messages are processed in the exact order they were sent
- **Example:** Producer sends 1, 2, 3, 4 → Consumer receives 1, 2, 3, 4
- **Standard Queue:** Messages may be processed out of order
- **FIFO Queue:** Guarantees message ordering

---

## 🛠️ Hands-On: Creating and Using an SQS Queue

### **Step 1: Create a Queue**
1. Navigate to SQS console
2. Click **Create queue**
3. Choose **Standard queue**
4. Enter queue name (e.g., `demo-sqs`)
5. Leave configuration and access policy as default
6. Click **Create queue**

### **Step 2: Send Messages**
1. Click **Send and receive messages**
2. Enter message body (e.g., "hello world")
3. Click **Send message**
4. Message status: **Ready to be delivered**
5. Send additional messages to see queue depth increase

### **Step 3: Receive Messages**
1. Click **Poll for messages** to retrieve messages from queue
2. Messages appear in the receive messages section
3. Click on a message to view:
   - **Body** – Message content
   - **Message ID** – Unique identifier
   - **MD5 attributes** – Message integrity

### **Step 4: Process and Delete Messages**
1. After processing (in real application, your code would handle this)
2. Select messages and click **Delete**
3. Messages are removed from queue
4. **Messages available** count returns to zero

### **Key Observations**
- **Messages available** – Shows pending messages in queue
- **Messages in flight** – Messages being processed
- **Messages delayed** – Messages scheduled for later delivery
- Queue details show type, name, encryption status

---

## 📊 Summary

| Feature | Description |
|---------|-------------|
| **Type** | Fully managed, serverless queue service |
| **Purpose** | Decouple applications |
| **Scaling** | Seamless, from 1 to tens of thousands of messages/second |
| **Retention** | 4 days default, 14 days maximum |
| **Latency** | Less than 10ms |
| **Queue Types** | Standard (no ordering) or FIFO (ordered) |

---

## 🎯 Key Takeaways

✅ **Queue model:**
- Producers send messages → Queue stores them → Consumers poll and process

✅ **Key features:**
- Fully managed, serverless
- Seamless scaling (1 to tens of thousands messages/second)
- Low latency (< 10ms)
- Message retention: 4 days default, 14 days max

✅ **Use case:** Decouple application tiers (e.g., web servers and video processing) for independent scaling

✅ **FIFO queues:** Guarantee message ordering (First In, First Out)

✅ **Horizontal scaling:** Multiple consumers share work and scale independently

---


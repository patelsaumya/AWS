# 🌐 Amazon API Gateway Overview

## 📋 Overview

**Amazon API Gateway** is a fully managed service that allows developers to easily create, publish, maintain, monitor, and secure APIs in the cloud. It's a serverless technology that provides RESTful and WebSocket APIs, making it easy to expose Lambda functions and other backend services to external clients.

---

## 🔍 What is API Gateway?

**Amazon API Gateway** is a service that acts as a front door for applications to access data, business logic, or functionality from your backend services. It provides a RESTful HTTP API that external clients can use to interact with your serverless applications.

### 🔑 Key Characteristics

- **Fully managed** – AWS handles all infrastructure management
- **Serverless** – No servers to provision or manage
- **Fully scalable** – Automatically scales to handle traffic
- **RESTful APIs** – Supports REST API architecture
- **WebSocket APIs** – Supports real-time streaming of data
- **Security features** – User authentication, API throttling, API keys
- **Monitoring** – Built-in monitoring and logging

---

## 🏗️ Architecture: Serverless HTTP API

### 📊 Use Case: Exposing Lambda Functions

**Problem:** Lambda functions are not directly accessible as HTTP APIs by external clients.

**Solution:** API Gateway acts as a proxy between clients and Lambda functions.

**Architecture Flow:**
```
External Client → API Gateway → Lambda Function → DynamoDB
```

**Example: CRUD Operations:**
- **Read** – GET request to retrieve data
- **Create** – POST request to create data
- **Update** – PUT request to update data
- **Delete** – DELETE request to remove data

### 📊 How It Works

1. **Client sends HTTP request** to API Gateway endpoint
2. **API Gateway receives request** and routes it to appropriate Lambda function
3. **Lambda function executes** business logic (e.g., CRUD operations)
4. **Lambda interacts with DynamoDB** to read/write data
5. **Response flows back** through API Gateway to client

---

## 🎯 Use Cases

### 📊 Serverless HTTP API

**Scenario:** Build a serverless API using Lambda and DynamoDB

**Components:**
- **API Gateway** – Exposes REST API to clients
- **Lambda Functions** – Handle business logic
- **DynamoDB** – Store and retrieve data

**Benefits:**
- **Fully serverless** – No infrastructure management
- **Scalable** – Automatically handles traffic spikes
- **Cost-effective** – Pay only for API calls
- **Secure** – Built-in authentication and authorization

### 📊 Real-Time Applications

**WebSocket APIs:**
- **Real-time streaming** – Bidirectional communication
- **Live data updates** – Push updates to clients
- **Chat applications** – Real-time messaging
- **Gaming** – Real-time game state updates

---

## 🔒 Security Features

### 📊 API Gateway Security

- **User Authentication** – Authenticate users before allowing API access
- **API Throttling** – Limit number of requests per second
- **API Keys** – Control access using API keys
- **Monitoring** – Track API usage and performance
- **Request Validation** – Validate request parameters
- **CORS Support** – Cross-Origin Resource Sharing configuration

---

## 🔗 Integration with AWS Services

### 📊 Common Integrations

**Lambda Functions:**
- **Primary use case** – Expose Lambda functions as REST APIs
- **Event-driven** – API Gateway triggers Lambda on HTTP requests

**Other Backend Services:**
- **EC2** – Connect to EC2 instances
- **ECS/Fargate** – Connect to containerized applications
- **HTTP Endpoints** – Connect to any HTTP backend
- **AWS Services** – Direct integration with other AWS services

---

## 📊 API Types

### 📊 REST APIs

**RESTful Architecture:**
- **HTTP Methods** – GET, POST, PUT, DELETE, PATCH
- **Resource-based URLs** – `/users`, `/products`, etc.
- **Stateless** – Each request is independent
- **JSON/XML** – Standard data formats

### 📊 WebSocket APIs

**Real-Time Communication:**
- **Bidirectional** – Client and server can send messages
- **Persistent Connection** – Maintains connection for real-time updates
- **Low Latency** – Fast message delivery
- **Use Cases** – Chat, gaming, live updates

---

## 💰 Pricing Model

### 📊 API Gateway Pricing

**REST APIs:**
- **Pay per API call** – Based on number of requests
- **Free tier** – First 1 million requests per month (free)
- **Data transfer** – Pay for data transfer out

**WebSocket APIs:**
- **Pay per connection** – Based on connection minutes
- **Free tier** – First 1 million connection minutes per month (free)
- **Messages** – Pay per million messages

---

## 📊 Summary

| Feature | Description |
|---------|-------------|
| **Service Type** | Fully managed API service |
| **Architecture** | Serverless, scalable |
| **API Types** | REST APIs, WebSocket APIs |
| **Primary Use** | Expose Lambda functions as HTTP APIs |
| **Security** | Authentication, throttling, API keys |
| **Integration** | Lambda, EC2, ECS, HTTP endpoints |
| **Monitoring** | Built-in monitoring and logging |
| **Pricing** | Pay per API call/connection |

---

## 🎯 Key Takeaways

- **API Gateway exposes Lambda as HTTP API** – Makes Lambda functions accessible via REST API
- **Fully managed service** – No infrastructure management required
- **Serverless** – No servers to provision or manage
- **Fully scalable** – Automatically scales with traffic
- **RESTful APIs** – Supports standard REST architecture
- **WebSocket APIs** – Supports real-time bidirectional communication
- **Security features** – Authentication, throttling, API keys, monitoring
- **Common pattern** – API Gateway + Lambda + DynamoDB for serverless APIs
- **CRUD operations** – Read, Create, Update, Delete data through HTTP methods
- **Integration** – Works with Lambda, EC2, ECS, and other AWS services

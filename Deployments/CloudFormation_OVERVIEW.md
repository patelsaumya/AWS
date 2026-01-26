# ☁️ AWS CloudFormation Overview

## 📋 Overview

Welcome to this section on **Deploying and Managing Infrastructure at Scale**.

In this section, we'll see different ways to deploy your workloads onto AWS. **AWS CloudFormation** is a declarative way of outlining your AWS infrastructure for any resources, and most of them are supported.

---

## 🔍 What is CloudFormation?

**AWS CloudFormation** is an Infrastructure as Code (IaC) service that allows you to define and provision AWS infrastructure using declarative templates. You specify what resources you want (e.g., security groups, EC2 instances, S3 buckets, load balancers), and CloudFormation automatically creates them in the right order with the exact configuration you specify.

### 🔑 Key Characteristics

- **Declarative** – Define what you want, not how to create it
- **Automated provisioning** – Creates resources in the correct order
- **Infrastructure as Code** – All infrastructure defined in templates
- **Wide support** – Supports almost all AWS resources
- **Custom resources** – Can extend to unsupported resources
- **Visualization** – Can visualize templates using Infrastructure Composer

---

## 💡 Benefits of CloudFormation

### 🎯 Control & Governance

- **Infrastructure as Code** – Never create resources manually
- **Code review** – All changes must go through code review
- **Version control** – Templates can be versioned and tracked

### 💰 Cost Advantages

- **Automatic tagging** – Resources in a stack get consistent tags
- **Cost estimation** – Easily estimate costs of resources
- **Saving strategies** – Automate deletion/recreation (e.g., delete at 5 PM, recreate at 8 AM)

### ⚡ Productivity

- **Easy creation/deletion** – Create and destroy infrastructure on the fly
- **Diagram generation** – Automatically generates architecture diagrams
- **Declarative programming** – No need to figure out creation order
- **Reusability** – Leverage existing templates from the web

### 🔧 Flexibility

- **Broad support** – Supports almost all AWS resources
- **Custom resources** – Extend to unsupported resources via Lambda
- **Template reuse** – Use and modify existing templates

---

## 🏗️ How CloudFormation Works

1. **Define template** – Create a JSON or YAML template describing your infrastructure
2. **Create stack** – CloudFormation reads the template and creates a "stack"
3. **Automatic provisioning** – Resources are created in the correct dependency order
4. **Manage lifecycle** – Update or delete the entire stack as a single unit

### 📊 Example Template Structure

```yaml
Resources:
  SecurityGroup:
    Type: AWS::EC2::SecurityGroup
    Properties: ...
  
  EC2Instance1:
    Type: AWS::EC2::Instance
    Properties: ...
  
  EC2Instance2:
    Type: AWS::EC2::Instance
    Properties: ...
  
  S3Bucket:
    Type: AWS::S3::Bucket
    Properties: ...
  
  LoadBalancer:
    Type: AWS::ElasticLoadBalancingV2::LoadBalancer
    Properties: ...
```

---

## 📐 Infrastructure Composer

CloudFormation templates can be visualized using the **Infrastructure Composer** service, which shows:
- All resources in the template
- Relationships between components
- Architecture diagrams with connections

This helps understand how components are linked together in your architecture.

---

## 🛠️ Hands-On: Creating and Updating a CloudFormation Stack

### 📋 Prerequisites

1. **Set Region** – Ensure you're in **US East (N. Virginia) - us-east-1** region
   - The templates use region-specific resources (AMI IDs, Availability Zones)
   - AMI IDs are scoped within regions

### 🚀 Step 1: Create Initial Stack

1. **Navigate to CloudFormation** → Click **"Create stack"**

2. **Template Preparation:**
   - Choose **"Upload a template file"**
   - Select **"Choose file"** and upload your template

3. **Initial Template** (`0-just-EC2.yaml`):

```yaml
---
Resources:
  MyInstance:
    Type: AWS::EC2::Instance
    Properties:
      AvailabilityZone: us-east-1a
      ImageId: ami-0453ec754f44f9a4a
      InstanceType: t3.micro
```

4. **View in Application Composer:**
   - Click **"View in Application Composer"** (opens in new tab)
   - See visual representation: single EC2 instance component
   - Switch between YAML/JSON views

5. **Stack Configuration:**
   - **Stack name:** `demo-CloudFormation`
   - **Parameters:** None (no parameters defined yet)
   - **Tags:** Add tag `Name: CFDemo`
   - Click **"Next"** → **"Submit"**

6. **Observe Stack Creation:**
   - Watch **Events** tab – shows resource creation progress
   - Stack status changes to `CREATE_COMPLETE`
   - **Resources** tab shows created EC2 instance

7. **Verify in EC2 Console:**
   - Navigate to EC2 → Instances
   - Find `MyInstance` running
   - Verify: **Instance Type** = `t3.micro`
   - Verify: **AMI ID** matches template
   - Check **Tags** tab:
     - CloudFormation auto-tags: `aws:cloudformation:stack-name`, `aws:cloudformation:logical-id`, `aws:cloudformation:stack-id`
     - Custom tag: `Name: CFDemo`

### 🔄 Step 2: Update Stack with Enhanced Template

1. **Update Stack:**
   - In CloudFormation console, select stack → Click **"Update"**
   - Choose **"Replace current template"** → **"Upload a template file"**

2. **Enhanced Template** (`1-ec2-with-sg-eip.yaml`):

```yaml
---
Parameters:
  SecurityGroupDescription:
    Description: Security Group Description
    Type: String

Resources:
  MyInstance:
    Type: AWS::EC2::Instance
    Properties:
      AvailabilityZone: us-east-1a
      ImageId: ami-0453ec754f44f9a4a
      InstanceType: t3.micro
      SecurityGroups:
        - !Ref SSHSecurityGroup
        - !Ref ServerSecurityGroup

  # an elastic IP for our instance
  MyEIP:
    Type: AWS::EC2::EIP
    Properties:
      InstanceId: !Ref MyInstance

  # our EC2 security group
  SSHSecurityGroup:
    Type: AWS::EC2::SecurityGroup
    Properties:
      GroupDescription: Enable SSH access via port 22
      SecurityGroupIngress:
        - CidrIp: 0.0.0.0/0
          FromPort: 22
          IpProtocol: tcp
          ToPort: 22

  # our second EC2 security group
  ServerSecurityGroup:
    Type: AWS::EC2::SecurityGroup
    Properties:
      GroupDescription: !Ref SecurityGroupDescription
      SecurityGroupIngress:
        - IpProtocol: tcp
          FromPort: 80
          ToPort: 80
          CidrIp: 0.0.0.0/0
        - IpProtocol: tcp
          FromPort: 22
          ToPort: 22
          CidrIp: 192.168.1.1/32

Outputs:
  ElasticIP:
    Description: Elastic IP Value
    Value: !Ref MyEIP
```

3. **Provide Parameters:**
   - **Security Group Description:** `demo description`
   - Click **"Next"**

4. **Review Change Set:**
   - CloudFormation shows **Change Set Preview**
   - **New resources to be added:**
     - `MyEIP` (Elastic IP) – **Action:** Add
     - `SSHSecurityGroup` – **Action:** Add
     - `ServerSecurityGroup` – **Action:** Add
   - **Modified resources:**
     - `MyInstance` – **Action:** Modify
     - **Replacement:** `True` ⚠️
     - ⚠️ **Important:** Replacement = `True` means the EC2 instance will be **deleted and recreated** (any data on the instance will be lost)

5. **Submit Update:**
   - Click **"Submit"**
   - CloudFormation automatically determines creation order:
     - Creates security groups first (dependencies)
     - Then updates/replaces EC2 instance
     - Finally creates and attaches Elastic IP

6. **Observe Update Process:**
   - **Events** tab shows:
     - Security groups created first
     - `MyInstance` update: "Requested update requires creation of a new physical resource, hence creating one"
     - New EC2 instance created
     - Old instance terminated (cleanup)
     - Elastic IP created and attached

7. **Verify Resources:**
   - **EC2 Console:**
     - Two instances visible during update (old + new)
     - Old instance gets terminated
     - New instance running with security groups attached
   - **Elastic IPs:**
     - Navigate to EC2 → Elastic IPs
     - Find `MyEIP` created and tagged
     - Check instance **Networking** tab → Elastic IP attached
   - **Security Groups:**
     - Two security groups created:
       - `SSHSecurityGroup`: Port 22 open to 0.0.0.0/0
       - `ServerSecurityGroup`: Port 80 open to 0.0.0.0/0, Port 22 open to 192.168.1.1/32

8. **View Updated Architecture:**
   - In CloudFormation → **Template** tab → **"View in Application Composer"**
   - Visual diagram shows:
     - EC2 instance connected to Elastic IP
     - EC2 instance connected to two security groups

### 🗑️ Step 3: Delete Stack

1. **Important:** Never delete resources manually when using CloudFormation
   - Don't delete Elastic IPs, EC2 instances, or security groups manually
   - Always use CloudFormation to manage resources

2. **Delete Stack:**
   - Select stack → Click **"Delete"**
   - CloudFormation deletes all stack resources in the correct order
   - Resources are deleted based on dependencies (e.g., detach Elastic IP before deleting instance)

3. **Verify Deletion:**
   - Stack status changes to `DELETE_COMPLETE`
   - All resources removed from AWS account

### 🎓 Key Observations

✅ **Infrastructure as Code** – Code defines infrastructure, not manual clicks

✅ **Automatic Dependency Management** – CloudFormation creates resources in correct order

✅ **Change Sets** – Preview changes before applying (shows what will be added/modified/deleted)

✅ **Resource Replacement** – Some updates require resource replacement (data loss warning)

✅ **Automatic Cleanup** – Old resources automatically deleted during updates

✅ **Visualization** – Application Composer provides visual architecture diagrams

✅ **Tagging** – Automatic CloudFormation tags + custom tags applied to all resources

---

## 📊 Summary

| Aspect | Description |
|--------|-------------|
| **Type** | Infrastructure as Code (IaC) service |
| **Approach** | Declarative (define what you want) |
| **Format** | JSON or YAML templates |
| **Resource Support** | Almost all AWS resources |
| **Custom Resources** | Supported via Lambda |
| **Visualization** | Infrastructure Composer |
| **Key Benefit** | Automated, repeatable infrastructure deployment |

---

## 🎯 Key Takeaways

✅ **CloudFormation is the base of Infrastructure as Code on AWS**

✅ **Use CloudFormation when:**
- You need infrastructure as code
- You need to repeat architecture in different environments, regions, or AWS accounts
- You want automated, consistent deployments
- You need cost optimization through automated resource lifecycle management

✅ **Benefits include:**
- Infrastructure as Code with code review
- Cost advantages through tagging and automation
- Productivity through declarative programming
- Reusability of existing templates

✅ **Supports almost all AWS resources** – Use custom resources for unsupported ones

✅ **Automatically handles dependencies** – Creates resources in the correct order

---

## 🌐 Elastic IP vs Public IP

**Elastic IP** is a static, public IPv4 address that you can allocate to your AWS account and associate with EC2 instances. Unlike a **Public IP** (which is dynamically assigned and changes when you stop/start an instance), an Elastic IP remains constant even if you stop and restart your instance. This is essential for services that require a fixed public IP address, such as web servers, email servers, or any application where external systems need to connect using a consistent IP address. Elastic IPs are free when attached to a running instance, but incur a small hourly charge when allocated but not in use.


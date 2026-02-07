# 🔗 VPC Peering

## 📋 Overview

**VPC Peering** connects two VPCs privately using AWS's network infrastructure, making them behave as if they were part of the same network.

---

## 🔑 Key Characteristics

- **Private connectivity** – Connects two VPCs using AWS network
- **Same network behavior** – Peered VPCs behave as if on the same network
- **Non-overlapping CIDR** – VPC CIDR ranges must not overlap
- **Non-transitive** – Peering connections are not transitive (must create direct connections)

---

## 🏗️ How It Works

### **Peering Connection**

```
VPC A (10.0.0.0/16) ←→ VPC Peering Connection ←→ VPC B (172.31.0.0/16)
```

- **Direct connection** – VPC A and VPC B can communicate directly
- **Private routing** – Traffic stays on AWS network (not over internet)
- **Route tables** – Must add routes in both VPCs' route tables to enable communication

### **Architecture Example**

```
VPC A (10.0.0.0/16)
    ↕ (Peering Connection)
VPC B (172.31.0.0/16)
```

After peering, resources in VPC A can communicate with resources in VPC B as if they were on the same network.

---

## ⚠️ Important Requirements

### **CIDR Range Overlap**

- **Must not overlap** – VPC CIDR ranges cannot overlap
- **Example:**
  - ✅ VPC A: `10.0.0.0/16` and VPC B: `172.31.0.0/16` (can peer)
  - ❌ VPC A: `10.0.0.0/16` and VPC B: `10.0.0.0/16` (cannot peer - overlap)

### **Non-Transitive Peering**

- **Not transitive** – Peering connections do not automatically extend to other VPCs
- **Example:**
  - VPC A ↔ VPC B (peered)
  - VPC A ↔ VPC C (peered)
  - **VPC B and VPC C cannot communicate** (no direct peering)
  - **Solution:** Create separate peering connection between VPC B and VPC C

### **Transitive Example**

```
VPC A ←→ VPC B (peered)
VPC A ←→ VPC C (peered)
VPC B ←→ VPC C (NOT peered) ❌

Result: VPC B and VPC C cannot communicate
```

**To enable VPC B ↔ VPC C communication:**
- Create separate peering connection: VPC B ←→ VPC C

---

## 🔧 Configuration

### **Create Peering Connection**

1. **Select VPCs:**
   - **Requester VPC (Local VPC)** – Your VPC
   - **Accepter VPC** – VPC to peer with

2. **VPC Location:**
   - **Same account** – VPC in your AWS account
   - **Different account** – VPC in another AWS account
   - **Same region** – VPC in same region
   - **Different region** – VPC in different region (inter-region peering)

3. **VPC ID:**
   - Enter the VPC ID of the target VPC

4. **Accept connection:**
   - If peering with different account, the other account must accept
   - Once accepted, VPCs can communicate

### **Route Table Configuration**

After peering is established:
- **Add routes** in both VPCs' route tables
- **Route:** Target VPC CIDR → Peering connection
- **Example:**
  - VPC A route table: `172.31.0.0/16` → `pcx-xxxxx` (peering connection)
  - VPC B route table: `10.0.0.0/16` → `pcx-xxxxx` (peering connection)

---

## 🛠️ Hands-On

### **Step 1: Create Peering Connection**

1. Go to **VPC Console** → **Peering connections** → **Create peering connection**
2. **Configure settings:**
   - **Name:** Enter peering connection name
   - **Requester VPC (Local VPC):** Select your VPC
   - **Accepter VPC:**
     - **My account** – VPC in your account
     - **Another account** – VPC in different account
     - **Region:** Same region or different region (e.g., Cape Town, Africa)
   - **VPC ID:** Enter target VPC ID
3. Click **Create peering connection**

### **Step 2: Accept Peering Connection**

1. **Same account:** Connection is automatically accepted
2. **Different account:** Other account must accept the peering request
3. **Status:** Changes from "Pending acceptance" to "Active" when accepted

### **Step 3: Configure Route Tables**

1. **VPC A route table:**
   - Add route: VPC B CIDR → Peering connection ID
2. **VPC B route table:**
   - Add route: VPC A CIDR → Peering connection ID
3. **Result:** Resources in both VPCs can now communicate

### **Key Observations**

- **VPC Peering = Private connection** – Uses AWS network (not internet)
- **CIDR must not overlap** – Cannot peer VPCs with overlapping IP ranges
- **Non-transitive** – Must create direct peering connection between each pair of VPCs
- **Route tables required** – Must add routes in both VPCs to enable communication
- **Cross-account/region** – Can peer VPCs in different accounts or regions

---

## 🎯 Key Takeaways

✅ **VPC Peering = Private connection** between two VPCs using AWS network

✅ **Same network behavior** – Peered VPCs behave as if on the same network

✅ **Requirements:**
- **CIDR ranges must not overlap** – Cannot peer VPCs with overlapping IP ranges
- **Route tables** – Must add routes in both VPCs to enable communication

✅ **Non-transitive:**
- Peering connections do not automatically extend to other VPCs
- If VPC A ↔ VPC B and VPC A ↔ VPC C, then VPC B and VPC C cannot communicate
- **Solution:** Create separate peering connection between VPC B and VPC C

✅ **Peering options:**
- **Same account** – VPC in your account
- **Different account** – VPC in another account (requires acceptance)
- **Same region** – VPC in same region
- **Different region** – Inter-region VPC peering

✅ **Use case:** Connect VPCs privately for resource communication (databases, applications, etc.)

---


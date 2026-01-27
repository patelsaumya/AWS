# 🔄 Amazon S3 Versioning

## 📋 Overview

**Amazon S3 Versioning** allows you to keep multiple variants of an object in the same bucket, enabling you to preserve, retrieve, and restore every version of every object stored in your bucket. This feature provides protection against accidental overwrites and deletions, making it easier to recover from user actions and application failures.

---

## 🔍 What is S3 Versioning?

**S3 Versioning** is a bucket-level setting that enables you to store multiple versions of the same object in a single bucket. When enabled, S3 automatically assigns a unique version ID to each object.

### ⚙️ How It Works

1. **Enable versioning** at the bucket level
2. **Upload a file** → S3 creates **Version 1** of that object
3. **Re-upload the same key** (overwrite) → S3 creates **Version 2**
4. **Upload again** → S3 creates **Version 3**, and so on

### 📂 Version Management

```
S3 Bucket (Versioning Enabled)
├── index.html (Version 3) ← Current
├── index.html (Version 2)
└── index.html (Version 1)
```

**Key Concept:** Instead of overwriting files, S3 creates new versions while preserving all previous versions.

---

## 🎯 Why Use S3 Versioning?

### ✅ Best Practice Benefits

**1. Protection Against Unintended Deletes**
- When you "delete" a file, S3 adds a **delete marker**
- Previous versions remain intact and can be restored
- No permanent data loss from accidental deletions

**2. Easy Rollback Capability**
- Roll back to any previous version
- Recover files from days, weeks, or months ago
- Restore to known good states after problems

**3. Change Tracking**
- See all modifications to objects over time
- Compare different versions
- Maintain audit trail of changes

---

## 🔄 Versioning States

### 🔓 Unversioned (Default)

- **Default state** for new buckets
- Only one version of each object exists
- No version IDs assigned

### ✅ Versioning Enabled

- **Multiple versions** of objects are stored
- Each object gets a **unique version ID**
- Previous versions are preserved

### ⏸️ Versioning Suspended

- **No new versions** created for new uploads
- **Previous versions remain** (safe operation)
- New objects get **version ID = null**

> 💡 **Important:** Suspending versioning does NOT delete previous versions - it's a safe operation.

---

## 📝 Version ID Behavior

### 🆔 Version ID Assignment

**Before Versioning Enabled:**
- Objects have **version ID = null**
- These objects remain unchanged when versioning is enabled

**After Versioning Enabled:**
- New uploads get **unique version IDs**
- Re-uploads create **additional versions** with new IDs

### 📊 Example Version Timeline

```
Timeline: Object "document.pdf"

Day 1: Upload document.pdf
       → Version ID: null (versioning disabled)

Day 2: Enable versioning on bucket

Day 3: Upload document.pdf (same name)
       → Version ID: xyz123 (new version)
       → Previous version (null) still exists

Day 4: Upload document.pdf again
       → Version ID: abc456 (newest version)
       → Previous versions (null, xyz123) still exist
```

---

## 🗑️ Deletion with Versioning

### 🔄 Delete Behavior

**When versioning is enabled:**
1. **Delete request** → S3 adds a **delete marker**
2. **Object appears deleted** in normal view
3. **All versions remain** in the bucket
4. **Can restore** by removing the delete marker

### 🔓 Permanent Deletion

To permanently delete versions:
- Must **explicitly delete each version** by version ID
- Only way to truly remove data from bucket
- Useful for compliance or storage cost management

---

## 💰 Cost Considerations

### 📊 Storage Costs

- **Each version counts** toward storage costs
- Multiple versions = multiple storage charges
- Monitor version accumulation over time

### 🎯 Cost Optimization Strategies

- **Lifecycle policies** – Automatically delete old versions
- **Manual cleanup** – Periodically remove unnecessary versions
- **Intelligent Tiering** – Move old versions to cheaper storage classes

---

## ⚙️ Versioning Configuration

### 🔧 Bucket-Level Setting

**Location:** Bucket Properties → Versioning
**Options:**
- **Disabled** (default)
- **Enabled**
- **Suspended**

### 🔄 State Transitions

```
Disabled → Enabled → Suspended
    ↑                    ↓
    └─── Cannot go back ─┘
```

> ⚠️ **Note:** Once versioning is enabled, you cannot return to "Disabled" state. You can only suspend it.

---

## 📊 Summary

| Feature | Description |
|---------|-------------|
| **Scope** | Bucket-level setting |
| **Purpose** | Store multiple versions of the same object |
| **Delete Protection** | Adds delete markers instead of permanent deletion |
| **Rollback** | Easy restoration to previous versions |
| **Version ID** | Unique identifier for each version |
| **Cost Impact** | Each version counts toward storage costs |
| **State Options** | Disabled, Enabled, Suspended |
| **Safety** | Suspending versioning preserves existing versions |

---

## 🧪 Hands-On: S3 Versioning in Action

### 📋 Overview

Enable versioning on your S3 bucket and experience version creation, rollback, and delete marker functionality.

---

### 📝 Step 1: Enable Versioning

#### 1️⃣ Access Versioning Settings

1. **Go to your S3 bucket** from previous labs
2. **Click Properties tab**
3. **Find "Bucket Versioning" section**
4. **Click "Edit"**

#### 2️⃣ Enable Versioning

1. **Select "Enable"** bucket versioning
2. **Save changes**
3. **Result:** Any file overwrites will now create new versions instead

---

### 📝 Step 2: Create Versions by Updating Files

#### 1️⃣ Test Your Website

1. **Find your website URL** from Properties → Static website hosting
2. **Visit your website** → Should see "I love coffee"

#### 2️⃣ Update Website Content

1. **Edit your `index.html` file** locally
2. **Change content:** "I love coffee" → **"I REALLY love coffee"**
3. **Save the updated file**

#### 3️⃣ Upload Updated File

1. **Go to Objects tab** in your bucket
2. **Upload** → **Add files**
3. **Select the updated `index.html`**
4. **Upload** (this will create a new version)

#### 4️⃣ Verify Update

1. **Refresh your website**
2. **Expected result:** Now shows "I REALLY love coffee"

---

### 📝 Step 3: View Versions

#### 1️⃣ Enable Version View

1. **In your bucket's Objects tab**
2. **Toggle "Show versions" ON**

#### 2️⃣ Observe Version Behavior

**What you'll see:**
- **Files uploaded before versioning** (beach.jpg, coffee.jpg) → **Version ID: null**
- **index.html** → **Two versions:**
  - **Version ID: null** (uploaded before versioning)
  - **Version ID: [unique-id]** (uploaded after versioning)

> 💡 **Key Insight:** Files existing before versioning enabled have **version ID = null**.

---

### 📝 Step 4: Roll Back Using Version Deletion

#### 1️⃣ Delete Specific Version

1. **Ensure "Show versions" is enabled**
2. **Click on the newest version** of `index.html` (with unique version ID)
3. **Click "Delete"**
4. **This is a permanent delete** → Cannot be undone
5. **Type "permanently delete"** in the confirmation box
6. **Delete the specific version**

#### 2️⃣ Verify Rollback

1. **Refresh your website**
2. **Expected result:** Back to "I love coffee" (previous version restored)

> ✅ **Success:** You've rolled back to the previous version by deleting the newer version!

---

### 📝 Step 5: Test Delete Markers

#### 1️⃣ Regular Delete (Creates Delete Marker)

1. **Turn OFF "Show versions"** (normal view)
2. **Select `coffee.jpg` file**
3. **Click "Delete"**
4. **Type "delete"** (not "permanently delete")
5. **Delete the object**

#### 2️⃣ Observe Delete Marker Behavior

**With versions hidden:**
- **coffee.jpg appears deleted** from the bucket

**With "Show versions" enabled:**
- **Delete marker** appears with its own version ID
- **Original coffee.jpg** still exists with version ID = null

#### 3️⃣ Test Website Impact

1. **Refresh your website**
2. **Force refresh:** Ctrl+Shift+R (Windows) or Cmd+Shift+R (Mac)
3. **Expected result:** Coffee image no longer displays
4. **Open image in new tab** → **404 Not Found error**

---

### 📝 Step 6: Restore from Delete Marker

#### 1️⃣ Delete the Delete Marker

1. **Ensure "Show versions" is enabled**
2. **Click on the delete marker** for coffee.jpg
3. **Click "Delete"**
4. **This permanently deletes the delete marker**
5. **Type "permanently delete"** and confirm

#### 2️⃣ Verify Restoration

1. **Return to your website**
2. **Refresh the page**
3. **Expected result:** Coffee image is back and displaying correctly

> ✅ **Success:** You've restored the file by removing the delete marker!

---

### 🔍 Key Observations

**Version Creation:**
- Overwriting files creates new versions instead of replacing
- Each version gets a unique version ID
- Pre-versioning files have version ID = null

**Delete Behavior:**
- **Permanent delete** → Removes specific version forever
- **Regular delete** → Creates delete marker, preserves actual data
- **Delete markers** can be removed to restore previous versions

**Rollback Capability:**
- Easy to revert to any previous version
- Website updates can be safely tested and rolled back
- No data loss when experimenting with changes

---

## 🎯 Key Takeaways

- **Enable at bucket level** – Versioning is configured per bucket
- **Automatic version creation** – No manual intervention needed
- **Protection against deletes** – Delete markers allow easy restoration
- **Easy rollback** – Return to any previous version
- **Version null** – Objects existing before versioning have version ID = null
- **Safe suspension** – Suspending versioning preserves all existing versions
- **Cost awareness** – Multiple versions increase storage costs
- **Best practice** – Recommended for important data and production buckets

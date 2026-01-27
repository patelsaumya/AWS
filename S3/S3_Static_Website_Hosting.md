# 🌐 Amazon S3 Static Website Hosting

## 📋 Overview

Amazon S3 can host **static websites** and make them accessible on the internet. This allows you to serve HTML files, CSS, JavaScript, images, and other static content directly from S3 buckets without traditional web servers.

---

## 🌐 Website URL Formats

The website URL depends on the **AWS region** where you create your bucket:

**Format 1 (with dash):**
```
http://bucket-name.s3-website-region.amazonaws.com
```

**Format 2 (with dot):**
```
http://bucket-name.s3-website.region.amazonaws.com
```

> 💡 **Note:** Both formats work similarly - the difference is just dash vs. dot separator.

---

## 🔓 Public Access Requirement

### ⚠️ Critical: Public Reads Required

Static website hosting **will not work** unless you have **public reads enabled** on your S3 bucket.

### 🚫 403 Forbidden Error

If you see a **403 Forbidden error** after enabling static website hosting:
- **Your bucket is not public**
- **You must attach an S3 bucket policy** that allows public access

---

## 📝 Required S3 Bucket Policy

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "PublicReadGetObject",
      "Effect": "Allow",
      "Principal": "*",
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::your-bucket-name/*"
    }
  ]
}
```

**This policy allows anyone to read all objects in your bucket.**

---

## ⚙️ Basic Configuration

- **Index Document:** `index.html` (required)
- **Error Document:** `error.html` (optional)
- **Public Access:** Disable "Block Public Access" settings
- **Bucket Policy:** Apply public read policy above

---

## 🎯 Use Cases

**✅ Good For:**
- Static websites (HTML, CSS, JS)
- Personal portfolios
- Documentation sites
- Single Page Applications (React, Angular, Vue.js)

**❌ Not For:**
- Dynamic websites with server-side processing
- User authentication/login systems
- Form processing
- E-commerce with databases

---

## 💰 Benefits

- **Cost-effective** – No server management, pay only for storage/transfer
- **Automatic scaling** – Handles any traffic volume
- **High availability** – Built-in redundancy
- **Simple deployment** – Just upload files

---

## 🧪 Hands-On: Enable Static Website Hosting

### 📋 Overview

Setting up static website hosting on an S3 bucket and testing the website functionality.

---

### 📝 Step 1: Prepare Files

#### 1️⃣ Upload Additional Files

1. **Go to your S3 bucket** from previous labs
2. **Upload files** for your website:
   - Upload `coffee.jpg` (or any image file)
   - Ensure you have content files in your bucket

> 💡 **Note:** You should have at least 2 files in your bucket before enabling website hosting.

---

### 📝 Step 2: Enable Static Website Hosting

#### 1️⃣ Access Website Settings

1. **Go to bucket Properties tab**
2. **Scroll all the way down** to find "Static website hosting"
3. **Click "Edit"**

#### 2️⃣ Configure Website Hosting

1. **Enable static website hosting** ✅
2. **Choose:** "Host a static website"
3. **Index document:** Enter `index.html`
4. **Error document:** (Optional) Enter `error.html`

> ⚠️ **Important Notice:** You'll see a warning that says "you must make all your content publicly readable" - this is why we learned about S3 bucket policies!

#### 3️⃣ Save Configuration

1. **Save changes**
2. **Note the bucket website endpoint** that appears

---

### 📝 Step 3: Upload Index Document

#### 1️⃣ Create Index File

You'll need an `index.html` file. Here's a simple example:

```html
<!DOCTYPE html>
<html>
<head>
    <title>My S3 Website</title>
</head>
<body>
    <h1>I love coffee</h1>
    <p>Hello world!</p>
    <img src="coffee.jpg" alt="Coffee image">
</body>
</html>
```

#### 2️⃣ Upload Index File

1. **Go back to Objects tab**
2. **Upload** → **Add files**
3. **Select your `index.html` file**
4. **Upload** and **close**

---

### 📝 Step 4: Get Website Endpoint

#### 1️⃣ Find Website URL

1. **Return to Properties tab**
2. **Scroll down to Static website hosting**
3. **Copy the bucket website endpoint URL**

#### 2️⃣ Test Your Website

1. **Paste the URL** in a new browser tab
2. **Expected result:** 
   - See "I love coffee"
   - See "Hello world!"
   - See your coffee.jpg image

> ✅ **Success:** Your static website is now live and accessible!

---

### 📝 Step 5: Test Individual Files

#### 1️⃣ Access Individual Objects

1. **Right-click on any image** in your website
2. **Open image in new tab**
3. **Verify:** You should see the public URL of your object

#### 2️⃣ Test Other Files

1. **Try accessing other files** directly:
   - `your-website-url/coffee.jpg`
2. **Result:** All files should be accessible via public URLs

---

### 🔍 Key Observations

**Website Endpoint Works:**
- Different URL format than regular S3 URLs
- Serves your `index.html` as the homepage
- All files publicly accessible

**Public Access Confirmed:**
- Images load directly in the browser
- Individual file URLs work
- Bucket policy enables public read access

**Files Served Directly:**
- No server processing needed
- Fast loading times
- Automatic scaling for traffic

---

## 🎯 Key Takeaways

- **Public access is mandatory** – 403 errors mean bucket isn't public
- **Bucket policy required** – Must allow `s3:GetObject` for public access
- **URL format varies by region** – Dash or dot separator
- **Static content only** – No server-side processing
- **Index document needed** – Usually `index.html`

# 🛡️ AWS IAM Security

## 📘 Overview

Now that we’ve created users and organized them into groups, it’s crucial to **protect these users from being compromised**.  
AWS provides two key defense mechanisms for securing your IAM users:

1. **Password Policy**
2. **Multi-Factor Authentication (MFA)**

This document explains both mechanisms and how they enhance account security.

---

## 🔐 1. Password Policy

A **Password Policy** defines the rules users must follow when setting or changing their passwords.  
A strong password policy reduces the risk of brute force or unauthorized access attacks.

### ✅ Key Configuration Options

| Setting | Description |
|----------|--------------|
| **Minimum Password Length** | Set a minimum number of characters (e.g., 8–12). |
| **Character Requirements** | Require a mix of uppercase, lowercase, numbers, and special characters. |
| **Allow IAM Users to Change Their Own Passwords** | Optionally allow users to update passwords without admin help. |
| **Password Expiration** | Require password changes after a specific period (e.g., every 90 days). |
| **Prevent Password Reuse** | Disallow reusing previous passwords. |

### 🧠 Why It Matters

- Enforces strong credentials for all IAM users.
- Protects against **brute-force** and **credential-stuffing** attacks.
- Keeps passwords fresh and hard to guess.

---

## 🧍‍♀️ 2. Multi-Factor Authentication (MFA)

While passwords are essential, they are **not enough**.  
MFA adds an **extra layer of security** by requiring two forms of authentication:

1. **Something you know** — your password
2. **Something you have** — a physical or virtual device

### 🔄 How It Works

For example, Alice uses her IAM password and an MFA code from her phone.  
Even if her password is stolen, her account remains secure unless the hacker also steals her MFA device.

---

## ⚙️ MFA Device Options in AWS

| Type | Description | Example |
|------|--------------|----------|
| **Virtual MFA Device** | Uses an app to generate time-based codes. | Google Authenticator, Authy |
| **U2F Security Key** | A physical USB/NFC key that authenticates the user. | YubiKey (by Yubico) |
| **Hardware Key Fob** | A small device that displays a rotating MFA code. | Gemalto Key Fob |
| **GovCloud Key Fob** | MFA device for AWS GovCloud users. | SurePassID |

### 💡 Notes
- **Virtual MFA devices** can store multiple accounts on one phone (e.g., Authy supports multiple tokens).
- **Physical keys** (like YubiKey) can be used across multiple AWS accounts or IAM users.
- Always enable MFA for your **root account** and **admin users**.

---

## 🧩 Benefits of MFA

- Protects accounts even if passwords are compromised.
- Greatly reduces the chance of unauthorized access.
- Simple to implement with existing mobile apps or hardware devices.

---

## 🚀 Summary

| Mechanism | Purpose | Example Feature |
|------------|----------|----------------|
| **Password Policy** | Strengthen password requirements | Minimum length, expiration |
| **MFA** | Add a second authentication factor | Virtual MFA, YubiKey |

Together, these two mechanisms form the **core of IAM user protection** in AWS.

## 🔨 Tools

- **IAM Credentials Report** (*account-level*) : Report that lists all you account's users and the status of their various credentials.
- **IAM Access Advisor / Last Access** (*user-level*) : Shows the service  permissions granted to a user and when those services were last accessed. Can be used to revise your policies.
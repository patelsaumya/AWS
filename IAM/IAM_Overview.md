# 🔐 IAM (Identity and Access Management)

IAM stands for **Identity and Access Management**. It is a **global service** in AWS that allows you to manage users, groups, and their permissions securely.

## 👑 Root User

When you create an AWS account, a **root user** is created by default. This is the primary account with full access.  
**Best Practice:** Use the root account only to set up your AWS environment. Avoid using it for daily tasks or sharing it.

## 👤 Users

A **user** represents a single person within your organization.
- Users can be grouped into **groups**.
- A user can belong to **multiple groups**.
- Some users may not belong to any group (though not recommended).

### 📝 Example

Organization with six people: Alice, Bob, Charles, David, Edward, Fred

- **Developers Group:** Alice, Bob, Charles
- **Operations Group:** David, Edward
- **Fred:** No group

### ⚠️ Key Points

- Groups can **only contain users**, not other groups.
- Users can belong to multiple groups (e.g., an audit team with Charles and David).

## 👥 Groups

Groups help manage **permissions collectively**.
- Assigning permissions to a group automatically applies them to all users within that group.
- Users or groups are assigned **policies** (JSON documents) that define their access.

## 📜 IAM Policies

An **IAM policy** is a JSON document that describes what actions a user (inline policy) or group can perform on AWS services.

### 🔧 Policy Structure

An IAM policy has a **JSON structure** with the following key components:

- **Version:** Policy language version (usually `"2012-10-17"`).
- **ID (optional):** Identifier for the policy.
- **Statements:** One or multiple statements describing permissions.

Each **statement** has:

1. **Sid (optional):** Statement ID.
2. **Effect:** `"Allow"` or `"Deny"` – determines whether access is granted or denied.
3. **Principal:** The user, group, or role to which the policy applies.
4. **Action:** The AWS API calls allowed or denied by this statement.
5. **Resource:** The resources on which actions are allowed or denied.
6. **Condition (optional):** Specifies when the statement applies.

Example policy snippet:

```json
{
  "Sid": "1",
  "Effect": "Allow",
  "Principal": {
    "AWS": "arn:aws:iam::987654321000:root"
  },
  "Action": [
    "s3:GetObject"
  ],
  "Resource": "arn:aws:s3:::my-shared-bucket/*"
}
```

If Policy 1 and 2 are assigned to the same user then this is what happens:

| Policy 1  | Policy 2  | Result            |
| --------- | --------- | ----------------- |
| Allow     | Allow     | Allowed           |
| Allow     | Deny      | Denied            |
| Deny      | Deny      | Denied            |
| Allow     | (nothing) | Allowed           |
| (nothing) | (nothing) | Denied (implicit) |


## ⛑️ Shared Responsibility Model

- **AWS**
  - Infrastructure (global network security)
  - Configuration and vulnerability analysis
  - Compliance validation
- **Customer**
  - Users, Groups, Roles, Policies management and monitoring
  - Enable MFA on all accounts
  - Rotate all your keys often
  - Use IAM tools to apply appropriate permissions
  - Analyze access patterns and review permissions


## ✅ Summary

- Create users for each person in your organization.
- Group users logically to simplify permission management.
- Assign policies to users or groups to control access to AWS services.
- Users can inherit multiple policies via multiple groups or inline policies.
- Avoid using the root account for daily operations.
- Follow the least privilege principle to ensure security.
# AWS Identity and Access Management (IAM)

## 1. What is IAM?

AWS Identity and Access Management (IAM) is the service that controls **who can access your AWS account and what they are allowed to do** inside it. IAM acts as the security foundation of AWS. Every request made to AWS—whether through the console, CLI, SDK, or an application—is first evaluated by IAM before it is allowed or denied.

Without IAM, every user and service would have full access to all AWS resources, which would be extremely unsafe and expensive. IAM ensures that access is granted strictly on a **need-to-do basis**, following the principle of least privilege.

**Key points:**
- IAM controls authentication and authorization
- IAM is global (not region-specific)
- IAM is free to use

---

## 2. Why IAM is Needed (Real-World Analogy)

Think of your AWS account as a company office building.

- The building itself is the AWS account
- Employees are IAM users
- Departments are IAM groups
- Temporary visitors or interns are IAM roles
- Office rules are IAM policies

Not everyone in the office can access payroll data, delete files, or enter the server room. IAM enforces similar rules inside AWS so that each person or service can only do what they are permitted to do.

---

## 3. IAM Users

An IAM user represents a **human user or an application** that needs access to AWS. Each user has unique credentials and can be assigned permissions directly or through groups.

IAM users can access AWS in two ways:
1. AWS Management Console (username + password)
2. Programmatic access (access key + secret key)

IAM users do not incur any additional cost.

**Example:**
- Admin user with full permissions
- Developer user with EC2 and S3 access
- Tester user with read-only access

**Key points:**
- IAM users are identities
- Credentials are unique per user
- Best practice: one IAM user per person

---

## 4. IAM Groups

IAM groups are collections of IAM users. Groups are used to **simplify permission management**. Permissions are assigned to groups, and users inherit permissions by being added to a group.

Instead of attaching policies individually to each user, you attach a policy to a group and add users to that group.

**Example:**
- Developers group → EC2 and S3 access
- Billing group → Billing and Cost Explorer access
- ReadOnly group → View-only permissions

**Key points:**
- Groups contain users
- Groups cannot contain other groups
- Users can belong to multiple groups

---

## 5. IAM Policies

IAM policies define **what actions are allowed or denied** on AWS resources. A policy is a JSON document evaluated every time a request is made.

Policies answer three main questions:
- What action is allowed or denied?
- On which AWS service?
- On which resource?

Policies can be attached to:
- Users
- Groups
- Roles

AWS evaluates policies using a strict rule:
**Explicit Deny always overrides Allow.**

**Example:**
A policy may allow reading objects from an S3 bucket but deny deleting them.

**Key points:**
- Policies control permissions
- Managed policies (AWS-managed or customer-managed)
- Inline policies are attached directly to one identity

---

## 6. IAM Roles (Very Important)

IAM roles are used to grant **temporary permissions** to trusted entities. Roles do not have long-term credentials like passwords or access keys.

Roles are commonly used by:
- EC2 instances
- Lambda functions
- ECS tasks
- Cross-account access

**Classic Exam Scenario:**
An EC2 instance needs access to S3.

Correct solution:
Attach an IAM role to the EC2 instance.

This avoids storing access keys and improves security by using automatically rotated temporary credentials.

**Key points:**
- Roles provide temporary access
- No credentials are stored
- Recommended for AWS services

---

## 7. Root User

The root user is created when you first create an AWS account. This user has **full, unrestricted access** to all AWS services and settings.

The root user cannot be restricted using IAM policies.

AWS strongly recommends:
- Do not use root user for daily tasks
- Enable Multi-Factor Authentication (MFA) immediately

**Exam Tip:**
If the question asks about unrestricted access → Root user

---

## 8. Multi-Factor Authentication (MFA)

MFA adds an additional layer of security by requiring:
1. Something you know (password)
2. Something you have (temporary code from an authenticator app)

MFA is especially important for:
- Root user
- IAM users with administrative or billing access

**Key points:**
- MFA improves account security
- Strongly recommended by AWS
- Common exam answer for security improvement

---

## 9. IAM and Other AWS Services (Exam Clarity)

IAM works alongside other AWS services but has a specific responsibility.

- IAM → Access control
- CloudTrail → Tracks API activity
- CloudWatch → Monitors performance and metrics
- Billing → Tracks cost and usage

IAM does not monitor or log activity; it only controls permissions.

---

## 10. IAM Pricing

IAM is completely free. You are not charged for:
- IAM users
- IAM groups
- IAM roles
- IAM policies

You only pay for the AWS services that IAM users and roles access.

---

## 11. IAM Best Practices

AWS recommends the following best practices:
- Enable MFA on the root account
- Do not use the root user for daily operations
- Grant least privilege permissions
- Use roles instead of access keys
- Regularly review permissions

---

## 12. Quick Exam Revision Summary

- IAM controls access to AWS
- Users represent people or applications
- Groups simplify permission management
- Policies define permissions
- Roles provide temporary access
- Root user has full access
- MFA adds security
- IAM is global and free

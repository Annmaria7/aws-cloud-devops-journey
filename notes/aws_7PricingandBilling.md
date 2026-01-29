# AWS Billing and Pricing – Cloud Practitioner Exam Prep

This document covers AWS Billing and Pricing concepts required for the **AWS Certified Cloud Practitioner (CLF-C02)** exam.  
The explanations are written in **complete sentences** first for understanding, followed by **summary bullets** for quick revision.

---

## 1. AWS Pricing Fundamentals

AWS follows a **pay-as-you-go pricing model**, which means you only pay for the services you use without any upfront cost or long-term commitment. This model allows customers to avoid large capital expenses and instead treat infrastructure as an operational expense.

AWS pricing is designed to be flexible so that customers can scale resources up or down based on demand and only pay for what they consume.

### Key Points
- No upfront payment required
- Pay only for what you use
- Scale up or down anytime
- No penalties for stopping services

---

## 2. Three Core AWS Pricing Principles

### Pay for What You Use
AWS charges you based on actual consumption, such as compute hours, storage used, or data transferred. If a service is stopped, billing for that service usually stops as well.

### Pay Less When You Use More
AWS offers **volume-based discounts**, meaning the per-unit cost decreases as usage increases. This applies to services like S3 storage and data transfer.

### Pay Less as AWS Grows
AWS continuously reduces prices as it benefits from economies of scale. These savings are often passed on to customers automatically without requiring any action.

### Key Points
- Metered usage-based billing
- Automatic volume discounts
- Price reductions over time

---

## 3. AWS Free Tier

AWS provides a **Free Tier** to help new users learn and experiment without immediate cost. The Free Tier is especially important for the Cloud Practitioner exam.

There are **three types of Free Tier offers**, and exam questions often test whether you understand the difference.

### Free Tier Types

#### Always Free
These services are free forever within defined limits.  
Example: AWS IAM, AWS VPC, AWS Lambda (limited requests).

#### 12 Months Free
These services are free for the first 12 months after account creation.  
Example: EC2 (750 hours of t2.micro), S3 (5 GB storage).

#### Trials
Short-term free trials that expire after a set time.  
Example: Amazon SageMaker Studio Lab (limited duration).

### Key Points
- Free Tier is account-based
- Usage beyond limits is charged
- Not all services are free

---

## 4. AWS Billing Dashboard

The **Billing Dashboard** is the central place where you view and manage AWS costs. It allows account owners to track current charges, past bills, and service-wise spending.

Only the **root user** or users with billing permissions can access billing information.

### What You Can Do in Billing Dashboard
- View current month charges
- Download invoices
- Track service-wise costs
- Manage payment methods

### Key Points
- Accessible via AWS Console → Billing
- Root user has full access
- IAM users need billing permissions

---

## 5. AWS Cost Allocation Tags

Cost Allocation Tags help you organize and track AWS costs by assigning metadata to resources. For example, you can tag resources by project, department, or environment.

Once activated in the Billing Dashboard, these tags appear in cost reports.

### Key Points
- Used for cost tracking and reporting
- Must be activated manually
- Helpful for organizations and teams

---

## 6. AWS Budgets

AWS Budgets allows you to set **custom cost and usage limits** and receive alerts when thresholds are exceeded. This helps prevent unexpected billing surprises.

Budgets can be configured to send notifications via email or Amazon SNS.

### Types of Budgets
- Cost budgets
- Usage budgets
- Reservation budgets

### Key Points
- Set monthly or custom budgets
- Alerts before overspending
- Exam favorite topic

---

## 7. AWS Cost Explorer

AWS Cost Explorer is a **visual cost analysis tool** that helps you understand historical spending patterns and forecast future costs.

It provides graphs and reports showing how much you spent on specific services over time.

### Key Points
- Visual graphs and charts
- Historical cost analysis
- Cost forecasting support

---

## 8. Consolidated Billing (AWS Organizations)

Consolidated Billing allows multiple AWS accounts to be managed under a single payer account using **AWS Organizations**. This is commonly used by enterprises.

It enables **combined usage discounts** and simplifies billing management.

### Key Points
- Single bill for multiple accounts
- Volume discounts across accounts
- Centralized cost management

---

## 9. AWS Pricing Calculator

The AWS Pricing Calculator helps estimate the cost of AWS services **before deploying resources**. This is useful for planning and budgeting.

The calculator provides cost breakdowns based on region, usage, and service configuration.

### Key Points
- Pre-deployment cost estimation
- Service-wise breakdown
- Exam-relevant tool

---

## 10. Support Plans and Pricing

AWS offers different **Support Plans**, and their pricing varies.

### Support Plans
- Basic (Free)
- Developer
- Business
- Enterprise

Only **Business and Enterprise** plans include full Trusted Advisor checks.

### Key Points
- Basic plan is free
- Paid plans cost a percentage of monthly usage
- Support level affects response time

---

## 11. Common Exam Traps (IMPORTANT)

AWS exams often test conceptual understanding rather than numbers.

### Typical Exam Scenarios
- “Which service helps track and forecast costs?” → Cost Explorer
- “Which tool sets spending limits?” → AWS Budgets
- “Who can access billing info by default?” → Root user
- “How do you estimate costs before launch?” → Pricing Calculator

---

## Final Revision Summary

- AWS uses pay-as-you-go pricing
- Free Tier has limits and categories
- Billing Dashboard shows current and past costs
- Budgets prevent overspending
- Cost Explorer analyzes and forecasts costs
- Consolidated Billing is for multi-account setups
- Pricing Calculator is for estimation before deployment

---

End of Billing & Pricing – Cloud Practitioner Prep

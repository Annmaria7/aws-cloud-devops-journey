# ALB + Microservices: Failure Scenarios and Solutions

## Base Architecture

ALB performs smart routing:

/users/* → Users Target Group

/orders/* → Orders Target Group

/payment/* → Payment Target Group

Each target group contains one or more EC2 instances (or ECS tasks/containers).

---

# Scenario 1: Single EC2 Instance Failure

Example:

Payment Target Group:

* EC2-1 ❌ Failed
* EC2-2 ✅ Healthy

## Impact

No user impact.

ALB health checks detect EC2-1 as unhealthy and stop sending traffic to it.

## AWS Solution

* ALB Health Checks
* Multiple targets in Target Group
* Auto Scaling Group replaces failed instance

## Exam Keywords

* High Availability
* Fault Tolerance
* Health Checks
* Auto Scaling

---

# Scenario 2: Entire Target Group Failure

Example:

Payment Target Group:

* EC2-1 ❌
* EC2-2 ❌
* EC2-3 ❌

HealthyHostCount = 0

## Impact

Only payment functionality becomes unavailable.

Users can still:

* Login
* Browse Products
* Search Products

But:

* Payments fail
* Checkout fails

Application appears partially healthy.

## AWS Solution

Infrastructure Side:

* Multi-AZ deployment
* Auto Scaling Groups
* Multiple instances/tasks

Monitoring Side:

* CloudWatch Alarms
* SNS Notifications
* HealthyHostCount monitoring

## Exam Keywords

* Multi-AZ
* CloudWatch Alarms
* SNS Notifications

---

# Scenario 3: Entire Availability Zone Failure

Example:

AZ-A

* Payment-1 ❌
* Payment-2 ❌

AZ-B

* Payment-3 ✅
* Payment-4 ✅

## Impact

No downtime if architecture is designed correctly.

ALB automatically routes traffic to healthy targets in surviving AZ.

## AWS Solution

* Multi-AZ ALB
* Multi-AZ Target Groups
* Auto Scaling across AZs

## Exam Keywords

* High Availability
* Multi-AZ
* Fault Tolerance

---

# Scenario 4: Infrastructure Healthy but Business Function Unavailable

Example:

Review Service unavailable.

Everything else works.

Users can:

* Login
* Browse Products
* Checkout

But cannot:

* View Reviews

## Impact

Application appears healthy.

Many users may never report the issue.

Can remain unnoticed.

## AWS Solution

Traditional Monitoring:

* CloudWatch Metrics
* CloudWatch Alarms

Advanced Monitoring:

* Synthetic Monitoring
* Canary Testing
* End-to-End Monitoring

Example:

Bot automatically:

Login → Search Product → Open Reviews

If Reviews fail:

Alert generated immediately.

## Exam Keywords

* CloudWatch Synthetics
* Monitoring
* Observability

---

# Scenario 5: Entire Microservice Dependency Failure

Example:

Payment Service depends on:

* DynamoDB
* SQS
* RDS

If dependency fails:

Payment service may become unusable even though EC2s remain healthy.

## Impact

ALB health checks may still show healthy.

Actual business operation fails.

## AWS Solution

* Dependency Monitoring
* CloudWatch Metrics
* Multi-AZ Databases
* Dead Letter Queues
* Redundancy

---

# Why ALB + Microservices Is Still Preferred

Without Microservices:

Each EC2 hosts:

* Users
* Orders
* Payments

This is a monolith.

Advantages:

* Fewer moving parts

Disadvantages:

* Scale entire application
* Larger deployments
* Larger blast radius

With Microservices:

Advantages:

* Independent scaling
* Independent deployment
* Better resource utilization
* Smaller failure domains

Disadvantage:

* Need strong monitoring and observability

---

# SAA Exam Summary

Remember:

ALB itself is NOT the problem.

The concern comes from Microservices Architecture.

AWS addresses these risks using:

* Health Checks
* Auto Scaling Groups
* Multi-AZ Deployments
* CloudWatch Alarms
* SNS Notifications
* CloudWatch Synthetics
* Monitoring and Observability

Key Principle:

"Application Up" ≠ "Every Feature Working"

Modern cloud architectures must monitor both infrastructure health and business functionality.

# NLB + ALB Combination Architecture

## Problem

### ALB (Application Load Balancer)

Advantages:

* Layer 7 Load Balancer
* Path-based routing
* Host-based routing
* Smart routing for microservices

Example:

/users/* → Users Service

/orders/* → Orders Service

/payments/* → Payments Service

Disadvantage:

* No Static Public IP Addresses
* IPs behind ALB can change

---

### NLB (Network Load Balancer)

Advantages:

* Layer 4 Load Balancer
* Static IP Addresses
* High Performance
* Low Latency

Disadvantage:

* No Path-based Routing
* No Host-based Routing
* No Smart Routing

---

## Solution

Use:

Client
↓
NLB (Static IPs)
↓
ALB (Smart Routing)
↓
Target Groups / Microservices

---

## Benefits of the Combination

### Benefit 1: Static IPs

Provided by NLB.

Useful when:

* Partner systems require IP whitelisting
* Banks require fixed source IPs
* Corporate firewalls allow only specific IPs

---

### Benefit 2: Smart Routing

Provided by ALB.

Examples:

/users/* → Users Target Group

/orders/* → Orders Target Group

/payments/* → Payments Target Group

Allows Microservices Architecture.

---

### Benefit 3: Independent Scaling

Each microservice can scale separately.

Example:

Heavy payment traffic:

Scale only Payment Service

instead of scaling the entire application.

---

### Benefit 4: High Availability

ALB performs health checks.

If a target becomes unhealthy:

Traffic is automatically routed to healthy targets.

Can be combined with:

* Auto Scaling Groups
* Multi-AZ Deployment

for fault tolerance.

---

## Typical Use Case

A third-party company says:

"Only traffic from IPs 52.10.10.10 and 52.10.10.11 is allowed."

Solution:

NLB provides fixed IPs.

ALB behind NLB provides:

* Path-based routing
* Host-based routing
* Microservice support

Result:

Static IPs + Smart Routing

Best of both worlds.

---

## Exam Shortcut

Need Static IPs?

→ NLB

Need Smart Routing?

→ ALB

Need BOTH?

→ NLB → ALB


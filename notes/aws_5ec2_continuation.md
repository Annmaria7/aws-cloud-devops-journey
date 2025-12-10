# EC2 Fundamentals – Lifecycle, Placement Groups & Pricing Models

---

# 🟣 1. EC2 Instance Lifecycle

An EC2 instance goes through multiple states from creation to termination.  
Understanding this is important for certification and real-world debugging.

## **Instance States**
| State | Meaning |
|-------|---------|
| **Pending** | Instance is launching. AWS is preparing resources. |
| **Running** | Instance is active and billing starts. |
| **Stopping** | Instance is preparing to stop. |
| **Stopped** | Instance is stopped; you are NOT billed for compute. (EBS volume billing continues.) |
| **Shutting-down** | Instance is preparing to terminate. |
| **Terminated** | Instance is permanently deleted. |

## **Stop vs Terminate**
- **Stop:**  
  - Instance shuts down  
  - EBS volume remains  
  - You can start again with same root volume  
  - Public IP **changes** unless using Elastic IP  
- **Terminate:**  
  - Entire instance + volumes are deleted  
  - Cannot restart

## **Reboot**
- Similar to OS restart  
- **No billing changes**  
- No IP change  
- No data loss

---

# 🟣 2. EC2 Placement Groups

Placement Groups enable control over the placement of EC2 instances for performance or redundancy needs.

## **Types of Placement Groups**

### ⭐ 1. Cluster Placement Group
Instances are placed *close together* in the same rack or AZ.

**Use Cases:**
- High-performance computing (HPC)
- Low-latency, high-throughput applications
- Big data jobs (Spark, Hadoop)

**Pros:**
- Very low latency  
- High network throughput  

**Cons:**
- Low fault tolerance  
- If rack fails → all affected

---

### ⭐ 2. Spread Placement Group
Instances are placed *on different underlying hardware*.

**Use Cases:**
- Critical applications needing high availability  
- Small number of instances (max 7 per AZ)

**Pros:**
- Best for **fault tolerance**  
- Hardware isolation  

**Cons:**
- Not suitable for large workloads  

---

### ⭐ 3. Partition Placement Group
Instances are divided into partitions; each partition uses different racks.

**Use Cases:**
- HDFS  
- HBase  
- Cassandra  
- Large distributed systems  

**Pros:**
- Isolation between partitions  
- Scales better than Spread  
- More resilient than Cluster  

**Cons:**
- Not as fast as Cluster

---

# 🟣 3. EC2 Purchase Options

Understanding pricing strategies helps optimize cost.

## ⭐ 1. On-Demand Instances
- No commitment  
- Pay per second/hour  
- Most expensive option  
- Good for testing, unpredictable workloads

**Analogy:** Hiring a taxi anytime.

---

## ⭐ 2. Reserved Instances (RIs)
Commit to 1 or 3 years → up to 72% discount.

Types:
- **Standard RI:** high discount, low flexibility  
- **Convertible RI:** less discount, can change instance family

**Good for:**
- Databases  
- Long-running workloads

---

## ⭐ 3. Savings Plans
Commit to spend `$X/hour` for 1–3 years.

Applies automatically to:
- EC2  
- Fargate  
- Lambda  

More flexible than RIs.

**Good for:**  
Teams with dynamic compute usage.

---

## ⭐ 4. Spot Instances
AWS gives unused capacity at up to 90% discount.  
Can be terminated anytime with **2-minute warning**.

**Use for:**  
- Machine Learning training  
- Batch jobs  
- Big data processing  
- Rendering  

**Avoid for:**  
- Production databases  
- Stateful apps

---

## ⭐ 5. Dedicated Hosts
You get an entire physical server.

**Use cases:**  
- Licensing (Oracle/Windows BYOL)  
- Compliance  
- Hardware-level isolation  

---

## ⭐ 6. Dedicated Instances
- Runs on dedicated hardware  
- Still shared across *your* instances  
- Not with external customers

---

## 🟢 Comparison Table

| Option | Cost | Commitment | Best For |
|--------|------|------------|----------|
| On-Demand | High | None | Short-term, testing |
| Reserved | Low | 1–3 years | Steady workloads |
| Savings Plans | Low | 1–3 years | Flexible workloads |
| Spot | Very Low | None | Fault-tolerant jobs |
| Dedicated Host | Very High | 1–3 years | Licensing & compliance |
| Dedicated Instance | High | None | Hardware isolation |

---
# Amazon Machine Image (AMI) – Full Notes

## 🧩 What is an AMI?
An **Amazon Machine Image (AMI)** is a **blueprint/template** used to create EC2 instances.  
It contains everything needed for a virtual machine to run.

### An AMI includes:
- Operating System (Ubuntu, Amazon Linux, Windows, etc.)
- Pre-installed software (Apache, Docker, Python, etc.)
- Configuration settings
- Permissions (who can use the AMI)

👉 **AMI = OS + Software + Configurations**

---

## 🎯 Why Do We Use AMIs?
Companies often need multiple identical servers.  
Manually installing OS + software again and again slows everything.

AMI solves this by:
- Launching identical servers instantly
- Ensuring consistency
- Reducing deployment time
- Enabling automation

---

## 🧃 Types of AMIs

### 1️⃣ AWS Provided AMIs
- Maintained by AWS  
- Secure, stable  
- Includes Amazon Linux, Ubuntu, Windows, RedHat

### 2️⃣ Marketplace AMIs
- Created by vendors  
- Often paid  
- Examples: Pre-configured WordPress, Jenkins, security tools

### 3️⃣ Community AMIs
- Shared by random users  
- **Not recommended** (security risk)

### 4️⃣ Custom AMIs (MOST important)
Created by **you** from a configured EC2 instance.

Example use cases:
- Auto Scaling Groups  
- Disaster recovery  
- Reusable production templates  
- Fast deployments  

---

## 🛠 How to Create a Custom AMI (High-Level)
1. Launch an EC2 instance  
2. Install required software  
3. Configure environment  
4. Stop the instance  
5. Go to: **Actions → Image → Create Image**  
6. AWS generates an AMI  
7. Launch new EC2 instances using this AMI

---

## 🍿 Real-World Example

### Netflix Example
Netflix needs **500 streaming servers**.

Steps:
1. Create 1 EC2 instance → install media engine, logs, security
2. Create AMI from it
3. Auto Scaling Group launches **hundreds of new servers** from this AMI based on traffic

Result:
- Faster deployments  
- Identical server behavior  
- Easy scaling  
- Fault tolerance  

---

## 🧠 Why AMIs Matter in Cloud/DevOps
- Used in CI/CD pipelines  
- Used in Auto Scaling Groups  
- Essential in disaster recovery  
- Enable immutable infrastructure  
- Reduce configuration drift  
- Speed up deployments  

---

## 🏁 Summary
- AMI is a machine template  
- Used to launch EC2 instances quickly & consistently  
- Custom AMIs are used in production everywhere  
- Key part of AWS compute and scalable architectures  

# AWS Elastic Load Balancers (ELB)

Load Balancers distribute traffic across multiple EC2 instances to increase availability, performance, and fault tolerance.

AWS offers **4 types of Load Balancers**:
- Application Load Balancer (ALB)
- Network Load Balancer (NLB)
- Classic Load Balancer (CLB)
- Gateway Load Balancer (GWLB)

---

# 1. Application Load Balancer (ALB)

**Layer:** 7 (Application Layer)  
**Use case:** Websites, web apps, APIs, microservices  
**Why:** ALB understands HTTP/HTTPS and supports smart routing.

### Features
- Path-based routing (`/login`, `/api`)
- Host-based routing (`api.example.com`)
- Header-based, query-based routing
- WebSockets support
- Works well with ECS, EKS (microservices)

### Diagram
```
               +----------------------+
User Request → |      ALB (Layer 7)   |
               +----------+-----------+
                          |
        ------------------------------------------------
        |                      |                      |
   Routes based on        Routes based on        Routes based on
      URL path             Hostname                Headers
    (/login)            (api.myapp.com)        (mobile=true)
        |                      |                      |
      EC2 A                 EC2 B                   EC2 C
```

### When to use ALB?
- You need smart routing  
- Your application is HTTP/HTTPS  
- You run microservices or container apps

---

# 2. Network Load Balancer (NLB)

**Layer:** 4 (Transport Layer)  
**Use case:** Extreme performance, low latency, TCP/UDP  
**Why:** NLB handles millions of requests per second.

### Features
- TCP/UDP load balancing
- Static IP support
- Ultra-low latency
- Preserves client IP

### Diagram
```
                +----------------------+
Traffic (TCP) → |     NLB (Layer 4)   |
                +----------+-----------+
                           |
                  Fast routing only
          ------------------------------------
          |                |                 |
        EC2 A            EC2 B             EC2 C
```

### When to use NLB?
- Gaming servers  
- Realtime trading apps  
- High-throughput backend  
- Load balancing databases  

---

# 3. Classic Load Balancer (CLB)

**Layer:** Basic Layer 4 + 7  
**Use case:** Only for legacy apps  
**Why:** Old generation of ELB; not recommended for new systems.

### When to use CLB?
- Only if migrating a very old application  
- Otherwise always pick ALB or NLB

---

# 4. Gateway Load Balancer (GWLB)

**Use case:** Security appliances  
**Why:** GWLB directs traffic through firewalls / IDS / IPS

### Diagram
```
          +-----------------------------+
Traffic → |     GWLB (Security Layer)   |
          +---------------+-------------+
                          |
                 Security Virtual Appliance
               (Firewall / Packet Inspector)
                          |
                        EC2
```

### When to use GWLB?
- Inserting firewalls between users and servers  
- Deep packet inspection  
- Security inspection workflows  

---

# Quick Comparison

| Load Balancer | Layer | Smart? | Best For |
|--------------|--------|--------|----------|
| **ALB** | L7 | Very smart | Websites, APIs, microservices |
| **NLB** | L4 | Super fast | TCP/UDP, high-performance apps |
| **CLB** | L4/L7 | Limited | Legacy apps |
| **GWLB** | Security | Specialized | Firewalls, packet inspection |

---

# Exam Quick Picks
- **Path-based routing?** → ALB  
- **TCP/UDP & performance?** → NLB  
- **Legacy application?** → CLB  
- **Firewall insertion?** → GWLB  

---


# ✅ End of Section  

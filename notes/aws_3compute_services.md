# ☁️ AWS Compute Services

> 🧠 **Concept Summary:**  
> Compute services in AWS provide the processing power for running applications, hosting websites, and performing data analysis — all without maintaining physical servers.  
> You choose how much control or automation you want: from **managing your own servers (EC2)** to **serverless code execution (Lambda)** or **fully managed containers (Fargate, ECS, EKS)**.

---

## 🖥️ 1. Amazon EC2 (Elastic Compute Cloud)
<details>
<summary>💡 Click to expand</summary>

### 🧾 Overview
Amazon EC2 offers **virtual machines (instances)** in the cloud. You have complete control over the operating system, configurations, and software stack.  
You can start or stop servers anytime and only pay for what you use.

### 🚀 When to Use
- You need **full control** over your environment.  
- You want to **install and configure** your own software.  
- You’re running **web apps, APIs, or databases** for long durations.  

### 🌍 Real-World Example
A small e-commerce website:
1. Launch a **Linux EC2 instance**.  
2. Install **Apache** or **Nginx**.  
3. Upload your website code.  
4. Access it via the EC2 public IP.  

When traffic spikes, add more instances using **Auto Scaling Groups**.

### ✅ Key Benefits
- Full OS control  
- Scalable and reliable  
- Integrated with Load Balancers and CloudWatch  
- Pay-as-you-go model  

# AWS EC2 — Simple & Beginner Friendly Notes

## 🌟 What is EC2?
EC2 is basically a **virtual computer** in AWS.
You can:
- Install software
- Run websites or apps
- Connect to it like your own computer

Think of it as **a computer you rent from AWS**.

---

# 1️⃣ EC2 Instances

An “instance” = your virtual computer.

### Instance Types (Hardware Options)
- **t2.micro / t3.micro** → small, free-tier  
- **m5.large** → balanced  
- **c5.large** → fast CPU  
- **r5.large** → more RAM  

You choose based on what you want to run.

---

# 2️⃣ What is an AMI?
AMI = **Amazon Machine Image**  
Think of an AMI like a **template** for your server.

It contains:
- Operating system (Ubuntu, Amazon Linux, Windows)
- Pre-installed software (sometimes)
- Settings

Example:
- If you choose **Ubuntu AMI**, your EC2 runs Ubuntu.

---

# 3️⃣ Security Groups (VERY Important)
Security Groups = **firewalls** for your EC2.

They decide:
- Who can enter the server
- Through which port
- From which IP

# AWS Security Groups — Simplified Notes

## 🚀 What is a Security Group?
A **Security Group (SG)** is a *virtual firewall* for your EC2 instance.  
It controls **which traffic is allowed IN and OUT** of your instance.

Think of it as **"who can talk to your EC2 and who your EC2 can talk to."**

---

## 🔐 Inbound Rules
These define **who can access your instance** and on **which port**.

Examples:
- Allow SSH from your own IP → only you can log in.
- Allow HTTP (port 80) → anyone can access your website.
- Allow HTTPS (port 443).

Inbound = *traffic coming in.*

---

## 📤 Outbound Rules
These define **where your instance is allowed to send traffic**.

Example:
- If outbound is "All traffic to 0.0.0.0/0" → your EC2 can access the internet.

Outbound = *traffic going out.*

---

## 🔁 Stateful Nature
Security Groups are **stateful**:

➡️ If an inbound request is allowed, the return traffic is automatically allowed —  
you **do NOT** need to add an outbound rule.

Example:  
If your laptop connects to EC2 via SSH, return SSH packets are automatically approved.

---

## 🌍 Example: SSH Safety
**Never allow SSH from 0.0.0.0/0** (full internet).  
Instead, allow:

```
Your Public IP/32
```

This keeps your instance safe from attacks.

---

## 🎯 Summary
| Feature | Meaning |
|--------|---------|
| Inbound | Who can access your EC2 |
| Outbound | Where your EC2 can send traffic |
| Stateful | Return traffic is automatically allowed |
| Default behavior | Deny all inbound, allow all outbound |

---

## 📝 Real-world Best Practices
- Allow SSH only from **your IP**
- Allow HTTP/HTTPS only for web servers
- Create separate SGs for DB tier, app tier, etc.
- Never leave unused open ports



---

# 4️⃣ Key Pair (.pem file)
When you launch EC2, AWS gives you a **.pem key**.

This key = **your password** to enter the EC2 through SSH.

- Without the key, you **cannot** access the instance.
- Keep it safe.
- Never upload it to GitHub.

---

# 5️⃣ Public vs Private IP

### Public IP
- Visible on the internet
- Used to connect from your laptop
- Changes when you stop/start instance (unless using Elastic IP)

### Private IP
- Used inside AWS network
- Not accessible from the internet
- Stays the same even if you restart the instance

------

## 🛠 How EC2 Works (Simple Explanation)

### **1️⃣ You launch EC2 from AWS console**
Choose:
- AMI (Ubuntu)
- Instance type (t2.micro)
- Key pair
- Security group

---

### **2️⃣ AWS gives it:**
- Private IP  
- (Optional) Public IP  
- Storage (EBS volume)

---

### **3️⃣ You log into the instance**
If Ubuntu:

```
ssh -i mykey.pem ubuntu@PUBLIC-IP
```

If Amazon Linux:

```
ssh -i mykey.pem ec2-user@PUBLIC-IP
```

---

### **4️⃣ You install apps**
Example:

```
sudo apt update
sudo apt install nginx -y
```

Now your Nginx website runs on the EC2.

---

### **5️⃣ You configure Security Group**
Allow inbound:
- **80 for HTTP**
- **443 for HTTPS**
- **22 for SSH (your IP only)**

---

### **6️⃣ You access your website**
Open browser → `http://PUBLIC-IP`

---

## 🏗 Real-World Example

### Example: Deploying a small website
1. Launch EC2 Ubuntu
2. Create SG → allow 22, 80
3. SSH into EC2
4. Install nginx
5. Upload your HTML files
6. Website is live globally 🚀

---

## 🧹 Stop = save money
EC2 is billed per running hour.  
Stop the instance to avoid charges.

---

## 🎯 Summary Table

| Concept | Meaning |
|--------|---------|
| AMI | Template for OS + config |
| Instance Type | Hardware power |
| SG | Firewall |
| Key Pair | Login credential |
| EBS | Storage disk for EC2 |
| Elastic IP | Permanent public IP |

---


</details>

---

## ⚡ 2. AWS Lambda (Serverless Compute)
<details>
<summary>💡 Click to expand</summary>

### 🧾 Overview
Lambda lets you **run code without managing servers**. You upload a function, define a trigger (like an API call or S3 event), and AWS handles the rest — provisioning, scaling, and execution.

### 🚀 When to Use
- Event-driven tasks  
- Automated workflows  
- Microservices and APIs  
- You only want to **pay for execution time**

### 🌍 Real-World Example
Your app allows image uploads.  
When a user uploads to **S3**, a **Lambda function**:
1. Resizes the image.  
2. Stores it back in S3.  
3. Sends a notification.

No server setup, no idle costs — just automatic function execution.

### ✅ Key Benefits
- Zero infrastructure management  
- Auto-scaled and highly available  
- Multi-language support (Python, Node.js, Java, etc.)  
- Pay per millisecond of execution  

</details>

---

## 🧩 3. AWS Fargate (Serverless Containers)
<details>
<summary>💡 Click to expand</summary>

### 🧾 Overview
AWS Fargate is a **serverless compute engine for containers**.  
It works with **ECS** and **EKS**, allowing you to run Dockerized applications without managing EC2 servers.

### 🌍 Real-World Example: *FoodFast App*
Your startup has:
- Frontend (React)
- Backend API (Node.js)
- Database (RDS)

You package your backend as a **Docker container** and push it to **ECR**.  
Then use **ECS with Fargate**:
- AWS runs your containers automatically.  
- No EC2 instances to manage.  
- Load balancer distributes traffic.  
- Scales automatically during rush hours.

### ✅ Key Benefits
- No server management  
- Scales automatically  
- Secure and isolated environments  
- Pay only for vCPU & memory usage  

</details>

---

## 🧱 4. Amazon ECS (Elastic Container Service)
<details>
<summary>💡 Click to expand</summary>

### 🧾 Overview
ECS is a **container orchestration service** to manage and scale containerized apps easily.  
You can run ECS:
- On **EC2** (you manage servers), or  
- On **Fargate** (AWS manages servers).

### 🌍 Example: Scalable Web API
You run a backend API using 3 containers. ECS automatically:
- Launches more containers if demand increases.  
- Replaces unhealthy ones.  
- Balances traffic across containers.

### ✅ Key Benefits
- Simplifies container management  
- Deep AWS integration (IAM, CloudWatch, VPC)  
- Flexible: EC2 or Fargate mode  
- Ideal for **microservice architectures**

</details>

---

## 🧭 5. Amazon EKS (Elastic Kubernetes Service)
<details>
<summary>💡 Click to expand</summary>

### 🧾 Overview
EKS is a **managed Kubernetes service**.  
You get the flexibility of open-source Kubernetes with the scalability of AWS.

### 🌍 Example: SaaS Platform
Your company has multiple services (auth, billing, notifications).  
Each service runs in containers managed by **Kubernetes**.  
EKS automatically handles:
- Cluster setup and scaling  
- Control plane updates  
- Integration with AWS security and networking

### ✅ Key Benefits
- Fully managed Kubernetes control plane  
- Works with EC2 or Fargate  
- Multi-cloud compatibility  
- Ideal for **enterprise-grade, complex systems**

</details>

---

## ⚖️ AWS Compute Comparison

| Service | Server Mgmt | Billing | Ideal For | Example Use Case |
|----------|--------------|----------|------------|------------------|
| 🖥️ **EC2** | Full control | Per uptime | Custom software or full-stack apps | Web apps, databases |
| ⚡ **Lambda** | None | Per execution | Event-driven logic | Image resize, data trigger |
| 🧩 **Fargate** | None | vCPU + memory | Containerized apps | APIs, microservices |
| 🧱 **ECS** | Optional | Depends on setup | Container orchestration | Web APIs, services |
| 🧭 **EKS** | Optional | Depends on setup | Kubernetes workloads | Enterprise apps |

---

## 🏠 Analogy Table

| Concept | Analogy |
|----------|----------|
| **EC2** | Renting a house 🏠 – full control, full responsibility |
| **Lambda** | Staying in a hotel 🏨 – pay only for your stay |
| **Fargate** | Renting a furnished apartment 🛋️ – AWS manages setup |
| **ECS** | Managing multiple furnished flats 🏢 – AWS helps orchestrate them |
| **EKS** | Managing an entire complex 🏙️ – full control via Kubernetes |

---

## ✅ Summary

- **EC2:** Run virtual servers with full control.  
- **Lambda:** Serverless functions triggered by events.  
- **Fargate:** Serverless containers for flexible scaling.  
- **ECS:** Orchestrate and scale containers.  
- **EKS:** Enterprise-grade Kubernetes management.

> 🪄 **Tip:**  
> Start small — experiment with **EC2** and **Lambda** first.  
> Then move to **containers (ECS/Fargate)**, and finally **EKS** for advanced Kubernetes workloads.

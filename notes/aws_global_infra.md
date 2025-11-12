# AWS Cloud Fundamentals: Global Infrastructure

## 1. What is Cloud Computing?
- Cloud computing provides **on-demand availability of computing resources** (data, applications, storage) over the internet.
- It is like a client-server model, but the server is **not physically near the client**.
- Benefits include **scalability, cost efficiency (pay-as-you-use), and high availability**.

## 2. Why Cloud vs On-Prem?
| Feature            | Cloud                                   | On-Prem                                      |
|-------------------|----------------------------------------|----------------------------------------------|
| Physical servers   | Abstracted; managed by cloud provider  | Located on-site, physically accessible       |
| Scalability        | Increase/decrease on demand            | Fixed capacity; upgrades required            |
| Cost               | Pay only for what you use              | Pay for full infrastructure regardless       |
| Traffic handling   | Automatic handling, can reduce congestion on the go | Needs manual planning and provisioning |
| Storage planning   | No need to pre-estimate storage        | Must estimate and provision storage ahead    |

## 3. What is AWS?
- **AWS (Amazon Web Services)** is a global cloud service provider.  
- Provides **compute, storage, networking, database, analytics, AI/ML**, and many other services worldwide.  

---

## 4. AWS Global Infrastructure Components

### 4.1 Regions
- Separate geographic areas with full AWS datacenters.  
- **Example:** Asia Pacific (Mumbai), US East (N. Virginia)  
- Regions allow users to **choose where their workloads and data reside**, improving compliance and latency.

### 4.2 Availability Zones (AZ)
- Isolated datacenters inside a region, with **independent power, networking, and cooling**.  
- Provides **fault tolerance**; if one AZ fails, others remain available.  
- **Example:** ap-south-1a, ap-south-1b

### 4.3 Edge Locations
- Small network endpoints close to users.  
- Mainly used for **content delivery via CloudFront** to reduce latency.  
- Do **not store origin data permanently**, only cached copies.  
- **Example:** Kochi Edge Location serves nearby users quickly without hitting the main region every time.

### 4.4 Regional Edge Cache (REC)
- Sits **between Edge Locations and the origin Region**.  
- Stores frequently accessed content to **reduce repeated requests to the origin AZ**.  
- Improves **latency and reduces load on the main datacenters**.  
- **Example:** If multiple users in Kerala repeatedly access the same video, Edge fetches it from REC instead of the origin every time.

### 4.5 Local Zones
- Extensions of a region deployed **near large population centers**.  
- Not full regions, but provide **compute, storage, and networking** for latency-sensitive workloads.  
- Useful for **gaming, media rendering, real-time analytics, and high-speed content delivery**.  
- **Example:** Los Angeles Local Zone allows apps to run with very low latency while still connecting to the parent region.

### 4.6 Outposts
- Fully managed AWS racks **delivered on customer premises**.  
- Let customers run **AWS services locally**, keeping low-latency access to on-site applications.  
- Ideal for **strict compliance, data residency, and high-security workloads**.  
- **Example:** A bank running sensitive financial processing locally while still using AWS services from the parent region.

---

## 5. ASCII Diagram: AWS Global Infrastructure

                   ┌─────────────────────┐
                   │      AWS Region     │  (e.g., Mumbai, US-East)
                   └─────────┬───────────┘
                             │
             ┌───────────────┴───────────────┐
             │                               │
    ┌───────────────┐                 ┌───────────────┐
    │ Availability  │                 │ Availability  │
    │ Zone (AZ)     │                 │ Zone (AZ)     │
    │ ap-south-1a   │                 │ ap-south-1b   │
    └───────────────┘                 └───────────────┘
             │                               │
             └─────────────┬─────────────────┘
                           │
                 ┌─────────┴─────────┐
                 │ Regional Edge Cache│
                 └─────────┬─────────┘
                           │
                ┌──────────┴──────────┐
                │  Edge Locations     │  (POP, e.g., Kochi)
                └──────────┬──────────┘
                           │
                   ┌───────┴─────────┐
                   │   Local Zones   │  (near cities, latency-sensitive)
                   └────────┬────────┘
                            │
                       ┌────┴─────┐
                       │ Outposts │  (AWS on-prem)
                       └──────────┘

---

## 6. Summary
AWS organizes its cloud globally for **availability, fault tolerance, and low latency**:  
- **Regions**: geographic areas with multiple AZs.  
- **Availability Zones**: isolated datacenters within a region.  
- **Edge Locations & Regional Edge Caches**: deliver content faster to end users.  
- **Local Zones**: mini-extensions near large cities for low-latency workloads.  
- **Outposts**: AWS infrastructure on customer premises for compliance and security.  

---


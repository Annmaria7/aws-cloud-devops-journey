# Why Do We Need Host-Based Routing If Path-Based Routing Exists?

## Initial Thought

While studying ALB, I learned:

ALB supports:

* Path-Based Routing
* Host-Based Routing

Example:

### Path-Based Routing

company.com/users

company.com/orders

company.com/payments

ALB Rules:

/users/* → Users Target Group

/orders/* → Orders Target Group

/payments/* → Payments Target Group

At first glance, this seems sufficient.

Question:

"If path-based routing can already route to different microservices, why do we need host-based routing at all?"

---

# Step 1: Understanding Microservices

Suppose a company has:

* User Service
* Order Service
* Payment Service

Using Path-Based Routing:

company.com/users

company.com/orders

company.com/payments

ALB routes requests to the correct Target Group.

Advantages:

* Simple architecture
* One domain
* Usually one SSL certificate
* Easier management

At this stage, it feels like Host-Based Routing is unnecessary.

---

# Step 2: Understanding SSL Certificates

Next question:

"What is the purpose of SSL certificates?"

SSL certificates provide:

1. Website Identity

Example:

Certificate proves:

"I am company.com"

2. Encryption Setup

Allows browser and server to establish an encrypted HTTPS connection.

Important:

Certificates verify domains, NOT microservices.

Certificate does NOT prove:

"I am Payment Service"

Certificate proves:

"I am payments.company.com"

This distinction is important.

---

# Step 3: Understanding SNI

Suppose ALB hosts:

payments.company.com

orders.company.com

users.company.com

Each domain may have its own SSL certificate.

Problem:

When browser connects:

How does ALB know which certificate to present?

Solution:

SNI (Server Name Indication)

Browser sends:

"I want payments.company.com"

during TLS handshake.

ALB chooses:

Payments Certificate

TLS connection is established.

Key Realization:

SNI helps ALB choose the correct certificate.

SNI does NOT choose the Target Group.

Target Group routing happens later.

---

# Step 4: Certificate Selection vs Traffic Routing

These are two separate decisions.

Decision 1:

Which certificate should ALB present?

Solved by:

SNI

Decision 2:

Which backend service should handle the request?

Solved by:

ALB Routing Rules

This was a major realization.

---

# Step 5: The Big Question

If path-based routing already works:

company.com/users

company.com/orders

company.com/payments

Why introduce:

users.company.com

orders.company.com

payments.company.com

which requires:

* Multiple certificates
* SNI
* More complexity

---

# Step 6: Real Business Requirements

The answer is:

Because sometimes businesses are not exposing multiple microservices.

They are exposing multiple products, brands, or websites.

---

# Scenario A: API Platform

Company has:

* User API
* Order API
* Payment API

Users never see these URLs directly.

Perfect candidate:

api.company.com/users

api.company.com/orders

api.company.com/payments

Path-Based Routing is ideal.

One certificate.

Simple.

---

# Scenario B: Multiple Public Websites

Company owns:

* Shop Website
* Blog Website
* Support Portal

Users expect:

shop.company.com

blog.company.com

support.company.com

Not:

company.com/shop

company.com/blog

company.com/support

Host-Based Routing becomes useful.

---

# Scenario C: SaaS Platform

Suppose Shopify.

Customers expect:

ann.shopify.com

john.shopify.com

mary.shopify.com

Instead of:

shopify.com/ann

shopify.com/john

shopify.com/mary

Host-Based Routing is the natural solution.

---

# Scenario D: Different Business Units

Company owns:

finance.company.com

hr.company.com

engineering.company.com

Each team may:

* Deploy independently
* Scale independently
* Use different backends

Host-Based Routing helps separate responsibilities.

---

# Scenario E: Multiple Domains

Company owns:

company.com

company.org

company.net

All point to the same ALB.

ALB routes:

company.com → Target Group A

company.org → Target Group B

company.net → Target Group C

Impossible using path-based routing alone.

---

# Final Understanding

Path-Based Routing and Host-Based Routing solve different problems.

Path-Based Routing:

Best for:

* APIs
* Internal services
* Microservices under one domain

Examples:

company.com/users

company.com/orders

company.com/payments

Advantages:

* Simpler
* Usually one certificate
* Easy management

---

Host-Based Routing:

Best for:

* Multiple websites
* SaaS platforms
* Multiple brands
* Multiple domains
* Team separation

Examples:

users.company.com

orders.company.com

payments.company.com

Advantages:

* Better branding
* Better organization
* Domain separation
* Supports multi-tenant architectures

Requires:

* Multiple certificates (often)
* SNI for certificate selection

---

# Exam Takeaway

Question:

"Which is better?"

Wrong approach.

Correct question:

"What business problem is being solved?"

If requirement is:

One domain, many APIs

→ Path-Based Routing

If requirement is:

Multiple websites, brands, tenants, or domains

→ Host-Based Routing

Neither is universally better.

They are tools for different architectural requirements.

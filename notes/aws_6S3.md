# AWS S3 – What We Have Covered So Far

This document contains **only the S3 concepts we have already covered**.
It is written for **hands-on understanding**, not exam theory.

You can upload this file directly to GitHub as:
aws-s3-notes.md

---

## What is Amazon S3?

Amazon S3 (Simple Storage Service) is an **object storage service** used to store
and retrieve **any amount of data** from anywhere.

Think of it like:
- Google Drive
- Dropbox
- But built for applications, not humans

---

## Core S3 Structure (Very Important)

S3 has a **simple hierarchy**:

Account  
└── Bucket  
    └── Object (file)

There are **no folders** in reality — folders are just prefixes.

---

## Buckets

A **bucket** is a container for objects.

### Bucket rules:
- Bucket names are **globally unique**
- Bucket names are **lowercase**
- No spaces or underscores
- Once created, **region cannot be changed**

Example bucket name:
my-app-user-images

---

## Objects

An **object** is the actual file you upload.

Each object consists of:
- File data
- Key (file path name)
- Metadata

Example object key:
images/profile/user1.jpg

---

## Object Size Limits

- Minimum: 0 bytes
- Maximum: 5 TB
- Single upload limit: 5 GB
- Larger files use **multipart upload**

---

## S3 is NOT a File System

Important difference:

File system:
- Edit files in place
- Hierarchy is real

S3:
- Objects are immutable
- You replace objects, not edit
- “Folders” are just names

---

## Bucket Region

- Every bucket belongs to **one AWS region**
- Data stays in that region unless replicated
- Region impacts:
  - Latency
  - Cost
  - Compliance

---

## S3 Storage Classes (Intro Level)

We covered the idea, not deep pricing.

Common ones:
- Standard
- Intelligent-Tiering
- Standard-IA
- Glacier

Key idea:
Different classes = different **cost vs access frequency**

---

## S3 Access Control – High Level

There are **three main layers** of access control:

1. IAM (who can access)
2. Bucket Policy (what is allowed on bucket)
3. Object ACL (legacy, mostly avoided)

---

## IAM (Identity and Access Management)

IAM controls **WHO** can access S3.

Examples:
- Users
- Roles
- Services (EC2, Lambda)

IAM policies are:
- JSON-based
- Attached to identities
- Reusable

---

## When to Use IAM for S3

Use IAM when:
- Access is **inside your AWS account**
- EC2 or Lambda needs S3 access
- Users are part of your organization

Example:
EC2 → IAM Role → S3 Bucket

---

## Bucket Policies

Bucket policies control:
- WHO can access the bucket
- WHAT actions are allowed
- FROM WHERE (IP / account / VPC)

Bucket policies are:
- Resource-based
- Written in JSON
- Attached directly to bucket

---

## When to Use Bucket Policies

Use bucket policies when:
- Granting cross-account access
- Making bucket public
- Restricting access by IP
- Enforcing HTTPS only

---

## IAM vs Bucket Policy (Simple View)

IAM:
- Identity-based
- Used inside account

Bucket Policy:
- Resource-based
- Used for external or bucket-level rules

They often work **together**.

---

## Public Access Block

S3 has a **Public Access Block** setting.

Purpose:
- Prevent accidental public exposure

Best practice:
- Keep all 4 options enabled
- Disable only if intentionally public

---

## Versioning

Versioning keeps **multiple versions** of objects.

When enabled:
- Delete = adds delete marker
- Old versions still exist
- Helps with recovery

Important:
Versioning is **bucket-level**.

---

## Encryption (Basics)

S3 supports encryption:
- At rest
- In transit

At rest:
- SSE-S3
- SSE-KMS

In transit:
- HTTPS

---

## S3 Use Cases (What We Discussed)

Common real-world uses:
- Application file storage
- Image and video hosting
- Static website hosting
- Backup and archival
- Data lake storage

---

## Simple Mental Model

S3 is:
- Durable
- Scalable
- Not a disk
- Not a database

It stores objects and serves them **reliably**.

---

## End of Covered Content


# EC2 Access Methods — Complete Guide (SAA + Real World)

## 1. Comparison Table

| Method | Needs Public IP on EC2? | Inbound Ports Needed | Keys Needed | Security Level | Real-World Usage |
|--------|------------------------|---------------------|------------|---------------|----------------|
| SSH | Yes | 22 | Yes (.pem) | Low | Small setups |
| PuTTY | Yes | 22 | Yes (.ppk) | Low | Legacy Windows |
| EC2 Instance Connect | Yes | 22 | Temporary key | Medium | Moderate |
| Session Manager (SSM) | No | None | No | High | Very High |
| RDP (Windows) | Yes | 3389 | Password | Low | Windows servers |
| Bastion Host | No (target EC2) | 22 only on bastion | Yes | Medium-High | Very Common |
| VPN Access | No | No public inbound on EC2 | Not always | Very High | Enterprise standard |

---

## 2. SSH (Secure Shell)
- Direct connection using public IP
- Uses key pair (.pem)
- Port: 22
- Simple but not production-safe

---

## 3. PuTTY (Windows SSH Client)
- Same as SSH but Windows-friendly
- Uses .ppk format
- Mostly outdated in modern workflows

---

## 4. EC2 Instance Connect
- Browser-based SSH via AWS Console
- Temporary keys injected by AWS
- Still requires public IP + port 22

---

## 5. Session Manager (Recommended)
- Uses AWS Systems Manager
- No public IP required
- No inbound ports needed
- IAM-based access control
- Works via AWS Console or CLI

### Why it's popular:
- Zero open ports
- Fully auditable
- Works inside private subnets

---

## 6. RDP (Windows Instances)
- Remote Desktop Protocol
- Port: 3389
- Uses decrypted password from key pair
- Same security concerns as SSH

---

## 7. Bastion Host (Jump Server)

### Architecture:
Internet → Bastion Host → Private EC2

### Key Points:
- Only bastion has public IP
- Private instances stay isolated
- SSH allowed only from bastion security group

### Pros:
- Reduces attack surface
- Common architecture pattern

### Cons:
- Still SSH-based
- Needs maintenance

---

## 8. VPN Access

### Architecture:
Laptop → VPN → VPC → Private EC2

### Types:
- Client VPN (developers)
- Site-to-site VPN (office network)

### Pros:
- Very secure
- No exposed ports
- Works like corporate network

### Cons:
- Setup complexity
- Possible latency
- Additional cost

---

## Security Ranking (Weak → Strong)

1. SSH / RDP (public)
2. EC2 Instance Connect
3. Bastion Host
4. Session Manager
5. VPN + Private Subnets

---

## Exam Tips (SAA)
- Know SSH basics
- Understand bastion architecture
- Remember Session Manager advantages
- VPN = hybrid connectivity

---

## Real-World Recommendation
Avoid public SSH in production.
Use:
- Session Manager for cloud-native environments
- VPN or Zero Trust for enterprise setups

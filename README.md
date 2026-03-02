# AWS VPC Network Design & Subnetting Lab

## Overview

This project documents a hands-on AWS VPC networking lab designed to simulate real-world cloud network architecture and security engineering tasks. The lab covers IPv4 and IPv6 subnetting, public and private subnet design, route table configuration, and Internet Gateway setup across multiple availability zones.

All configurations were performed in a live AWS environment using the AWS Management Console.

---

## Skills Demonstrated

- VPC design and deployment from scratch
- IPv4 CIDR subnetting and address space planning
- IPv6 dual stack networking and /64 subnet assignment
- Public and private subnet architecture
- Route table creation and traffic flow configuration
- Internet Gateway attachment and routing
- High availability design across multiple availability zones
- Private subnet isolation verification and security auditing

---

## Network Architecture

```
VPC: 10.0.0.0/16  (65,536 IPv4 addresses)
│
├── public-subnet-1  — 10.0.1.0/24 — us-east-2a — Internet routable 
├── public-subnet-2  — 10.0.2.0/24 — us-east-2b — Internet routable 
├── private-subnet-1 — 10.0.3.0/24 — us-east-2a — Isolated 
└── private-subnet-2 — 10.0.4.0/24 — us-east-2b — Isolated 
IPv6 Dual Stack (/64 per subnet)
├── public-subnet-1  — 2600:1f16:b2b:300::/64 — ::/0 routed via IGW 
├── public-subnet-2  — 2600:1f16:b2b:302::/64 — ::/0 routed via IGW 
├── private-subnet-1 — 2600:1f16:b2b:301::/64 — Local only 
└── private-subnet-2 — 2600:1f16:b2b:303::/64 — Local only
```

---

## Modules

| Module | Topic | Key Concepts |
|--------|-------|-------------|
| [Module 1](./module-1-ip-foundations.md) | IP Addressing Foundations | IPv4, CIDR notation, subnetting math, private address ranges |
| [Module 2](./module-2-network-design.md) | Network Design | Subnet planning, address space allocation, high availability |
| [Module 3](./module-3-vpc-subnets.md) | VPC and Subnet Creation | VPC deployment, subnet carving, availability zones |
| [Module 4](./module-4-public-private.md) | Public vs Private Subnets | Internet Gateway, route tables, subnet isolation |
| [Module 5](./module-5-ipv6.md) | IPv6 Dual Stack | IPv6 CIDR assignment, dual stack routing, security implications |

---

## Real-World Relevance

**Module 1 & 2** reflect the planning and design phase that network and cloud security engineers perform before touching any infrastructure. Understanding subnetting math is a core requirement for both the CompTIA Network+ exam and any cloud networking role.

**Module 3** demonstrates the foundational VPC deployment pattern used in virtually every production AWS environment. The four-subnet design across two availability zones is the AWS standard high availability architecture.

**Module 4** covers the routing configuration that determines whether a subnet is truly public or private. Misconfigured route tables that expose private subnets to the internet are a leading cause of cloud security incidents.

**Module 5** introduces dual stack networking — running IPv4 and IPv6 simultaneously — which is the current industry standard. A common security mistake is locking down IPv4 while leaving IPv6 uncontrolled, creating an exploitable gap that attackers specifically target.

---

## Screenshots

All lab screenshots are located in the [`/screenshots`](./screenshots/) directory, organized by module.

---

## Tools & Services Used

- AWS VPC
- AWS Internet Gateway
- AWS Route Tables
- AWS Subnets
- IPv4 CIDR Subnetting
- IPv6 Dual Stack Networking



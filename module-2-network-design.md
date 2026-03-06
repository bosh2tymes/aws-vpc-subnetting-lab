# Module 2 — Network Design

[← Back to Main README](./README.md)

## Objective

Design the full VPC network architecture on paper before building anything in AWS. Understanding what you're building and why before touching the console is a professional habit that prevents costly mistakes.

---

## Background

A VPC (Virtual Private Cloud) is an isolated virtual network in AWS that you define and control. Every resource you launch in AWS lives inside a VPC. The design decisions you make at this stage, (address space, subnet sizing, availability zones, and public vs private separation) are difficult or impossible to change after deployment.

---

## Network Design

### VPC
```
| Name | lab-vpc |
| IPv4 CIDR | 10.0.0.0/16 |
| IPv6 CIDR | Amazon-provided /56 |
| Total IPv4 addresses | 65,536 |
```

The `/16` was chosen to give plenty of room to carve multiple subnets while staying within a clean, readable address space. In production environments engineers think carefully about VPC sizing because the CIDR block cannot be changed after creation.

```
### Subnet Design

| Subnet | CIDR | Availability Zone | Type |
|--------|------|-------------------|------|
| public-subnet-1 | 10.0.1.0/24 | us-east-2a | Public |
| public-subnet-2 | 10.0.2.0/24 | us-east-2b | Public |
| private-subnet-1 | 10.0.3.0/24 | us-east-2a | Private |
| private-subnet-2 | 10.0.4.0/24 | us-east-2b | Private |
```
---
## Design Decisions Explained

### Why 10.0.0.0/16 for the VPC?

`10.0.0.0/16` is the most common VPC CIDR block used in production AWS environments. It gives 65,536 addresses to work with, and leaves the third octet free to use as a subnet identifier making the network easy to read and troubleshoot.

### Why /24 for each subnet?

Each `/24` provides 251 usable addresses — enough for any reasonably sized workload tier while keeping subnets small enough to enforce clean boundaries between tiers. Using consistent `/24` subnets across all four keeps the design simple and readable.

### Why increment the third octet?

Using `10.0.1.x`, `10.0.2.x`, `10.0.3.x`, `10.0.4.x` is a deliberate convention. Anyone looking at an IP address in this VPC can immediately identify which subnet it belongs to just from the third octet. That readability matters during incidents when engineers are under pressure.

### Why two availability zones?

An availability zone is a physically separate data center within an AWS region. Spreading subnets across `us-east-2a` and `us-east-2b` means the application keeps running in one AZ if the other experiences an outage. 

### Why separate public and private subnets?

Public subnets host resources that need to be reachable from the internet (web servers, load balancers, bastion hosts). Private subnets host resources that should never be directly reachable from the internet (databases, internal APIs, application servers). This separation is one of the most fundamental security controls in cloud architecture and is required by frameworks like PCI-DSS for any environment handling payment data.

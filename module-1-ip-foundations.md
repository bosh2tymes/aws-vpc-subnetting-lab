# Module 1 — IP Addressing Foundations

[← Back to Main README](./README.md)

## Objective

Build a foundational understanding of IPv4 addressing, CIDR notation, and subnetting math before configuring any AWS resources.Planning the network on paper first establishes a clear baseline 
understanding of the architecture, ensuring that every resource created in AWS has a deliberate purpose rather than being configured by trial and error.

---

## Background

An IPv4 address is a 32-bit number written as four octets separated by dots. Each octet is 8 bits and can represent a value from 0 to 255. Every device on a network needs a unique IP address to communicate.

CIDR notation expresses an IP address and its network prefix together. The number after the slash tells you how many bits are locked as the network portion. The remaining bits are available for host addresses within that network.

---

## Key Concepts Covered

### CIDR Notation and Subnet Sizing

```
| Prefix | Host Bits | Total Addresses | Usable in AWS |
|--------|-----------|----------------|---------------|
| /8 | 24 | 16,777,216 | 16,777,211 |
| /16 | 16 | 65,536 | 65,531 |
| /24 | 8 | 256 | 251 |
| /28 | 4 | 16 | 11 |
```

AWS reserves 5 addresses in every subnet:
- First address — network address
- Second address — AWS VPC router
- Third address — AWS DNS server
- Fourth address — reserved for future AWS use
- Last address — broadcast address


### Why Subnetting Matters

Subnetting divides a large network into smaller segments for three reasons:

- **Organization** — group related resources together logically
- **Security** — control traffic flow between segments using routing rules and firewalls
- **Efficiency** — reduce broadcast traffic and simplify network management

### Network vs Host Portion

For a device with IP `10.0.1.50` on a `/24` subnet:
```
10  .  0  .  1  .  50
|8 bits|8 bits|8 bits|8 bits|
|------24 bits------|8 bits|
|   NETWORK         | HOST |
```


Every device in `10.0.1.0/24` shares the same first 24 bits — `10.0.1`. Only the last 8 bits change to give each device a unique address within the subnet. Two devices on different /24 subnets cannot communicate directly without a router because their network portions differ.

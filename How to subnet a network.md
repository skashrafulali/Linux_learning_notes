# 📘 Subnetting Notes & Practice

## Core Concepts

**IP Address** = Network portion + Host portion  
**Subnet Mask** determines how many bits are network vs host.

### CIDR Notation
`/24` means 24 bits are network bits (e.g., `255.255.255.0`)

### Key Formulas
- **Number of subnets** = `2^(borrowed bits)`
- **Number of hosts per subnet** = `2^(host bits) − 2` (subtract network address + broadcast address)
- **Block size (increment)** = `256 − (last non-zero octet of subnet mask)`

### Common Subnet Mask Cheat Sheet

| CIDR | Subnet Mask       | Hosts/Subnet | Block Size |
|------|--------------------|--------------|------------|
| /24  | 255.255.255.0      | 254          | 256        |
| /25  | 255.255.255.128    | 126          | 128        |
| /26  | 255.255.255.192    | 62           | 64         |
| /27  | 255.255.255.224    | 30           | 32         |
| /28  | 255.255.255.240    | 14           | 16         |
| /29  | 255.255.255.248    | 6            | 8          |
| /30  | 255.255.255.252    | 2            | 4          |

### Steps to Subnet
1. Identify how many subnets or hosts you need.
2. Determine how many bits to borrow from the host portion.
3. Calculate the new subnet mask.
4. Find the block size (increment) to list subnet ranges.
5. For each subnet, identify: **Network ID, Usable Host Range, Broadcast Address**.

---

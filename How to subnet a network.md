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
## 🧮 Practice Questions (Different Approaches)

### Question 1 — Approach: Given Number of Subnets Needed

**Q:** You have the network `192.168.1.0/24`. You need **4 subnets**. Find the new subnet mask, block size, and list all subnets with their ranges.

**Answer:**
- Need 4 subnets → `2^n ≥ 4` → `n = 2` bits borrowed
- New mask: `/24 + 2` = **`/26`** = `255.255.255.192`
- Block size = `256 − 192` = **64**

| Subnet | Network ID      | Host Range       | Broadcast        |
|--------|-----------------|------------------|-------------------|
| 1      | 192.168.1.0     | .1 – .62         | .63               |
| 2      | 192.168.1.64    | .65 – .126       | .127              |
| 3      | 192.168.1.128   | .129 – .190      | .191              |
| 4      | 192.168.1.192   | .193 – .254      | .255              |

---
### Question 2 — Approach: Given Number of Hosts Needed

**Q:** You need a subnet that supports **50 hosts**. What is the smallest subnet mask you can use? Show the network for `10.0.0.0`.

**Answer:**
- Need 50 usable hosts → `2^h − 2 ≥ 50` → `h = 6` (`2^6 − 2 = 62`) ✅ (h=5 gives only 30, not enough)
- Host bits = 6 → Network bits = `32 − 6` = **`/26`** = `255.255.255.192`
- Block size = 64

**Result:** `10.0.0.0/26`
- Network ID: `10.0.0.0`
- Usable Hosts: `10.0.0.1 – 10.0.0.62`
- Broadcast: `10.0.0.63`

---

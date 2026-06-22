# 🛰️ Essential Nmap Commands Every Beginner Should Know

Nmap (Network Mapper) is one of the most powerful tools used by network administrators, system engineers, and cybersecurity professionals to discover hosts, identify open ports, detect services, and gather information about a target system.

---

# 1. Basic Host Discovery

```bash
nmap 192.168.1.1
```

### What it does

Scans the target host and shows open ports.

### Information obtained

* Host status (up/down)
* Open ports
* Services running on those ports

Example Output:

```
PORT    STATE SERVICE
22/tcp  open  ssh
80/tcp  open  http
443/tcp open  https
```

---

# 2. Scan Multiple Hosts

```bash
nmap 192.168.1.1 192.168.1.2
```

### What it does

Scans multiple IP addresses.

### Information obtained

* Which hosts are online
* Open ports on each host

---

# 3. Scan an Entire Subnet

```bash
nmap 192.168.1.0/24
```

### What it does

Scans every device in the subnet.

### Information obtained

* Active devices
* Open ports
* Running services

Useful for finding all devices connected to a network.

---

# 4. Ping Scan (Host Discovery Only)

```bash
nmap -sn 192.168.1.0/24
```

### What it does

Checks which hosts are alive without scanning ports.

### Information obtained

* Online devices
* MAC addresses (sometimes)
* Device vendors (sometimes)

Example:

```
Nmap scan report for 192.168.1.10
Host is up.
```

---

# 5. Scan Specific Ports

```bash
nmap -p 22,80,443 192.168.1.1
```

### What it does

Scans only selected ports.

### Information obtained

* Whether specified ports are open, closed, or filtered

Example:

```
22/tcp open ssh
80/tcp open http
443/tcp open https
```

---

# 6. Scan a Range of Ports

```bash
nmap -p 1-1000 192.168.1.1
```

### What it does

Scans ports 1 through 1000.

### Information obtained

* Open services within that range

---

# 7. Service Version Detection

```bash
nmap -sV 192.168.1.1
```

### What it does

Attempts to identify service versions.

### Information obtained

* Service names
* Software versions

Example:

```
22/tcp open ssh OpenSSH 8.9
80/tcp open http Apache httpd 2.4.57
```

---

# 8. Operating System Detection

```bash
sudo nmap -O 192.168.1.1
```

### What it does

Attempts to identify the target's operating system.

### Information obtained

* Linux/Windows/macOS
* Kernel details (sometimes)

Example:

```
OS details: Linux 5.x
```

---

# 9. Aggressive Scan

```bash
sudo nmap -A 192.168.1.1
```

### What it does

Combines multiple detection techniques.

### Information obtained

* Open ports
* Service versions
* Operating system
* Traceroute
* NSE script results

Useful for reconnaissance.

---

# 10. TCP SYN Scan (Stealth Scan)

```bash
sudo nmap -sS 192.168.1.1
```

### What it does

Performs a half-open TCP scan.

### Information obtained

* Open ports
* Filtered ports

Why it's popular:

* Faster
* Less noisy than a full TCP connection

---

# 11. UDP Scan

```bash
sudo nmap -sU 192.168.1.1
```

### What it does

Scans UDP ports.

### Information obtained

* DNS (53)
* DHCP (67/68)
* SNMP (161)
* Other UDP services

---

# 12. Scan All 65,535 Ports

```bash
sudo nmap -p- 192.168.1.1
```

### What it does

Scans every TCP port.

### Information obtained

* Hidden services
* Non-standard service ports

---

# 13. Detect Firewall Filtering

```bash
nmap -sA 192.168.1.1
```

### What it does

ACK scan used to analyze firewall rules.

### Information obtained

* Filtered ports
* Firewall presence

---

# 14. Fast Scan

```bash
nmap -F 192.168.1.1
```

### What it does

Scans only the most common ports.

### Information obtained

* Common services quickly

Useful when speed matters.

---

# 15. Save Results to a File

```bash
nmap -oN results.txt 192.168.1.1
```

### What it does

Saves scan results in normal text format.

Output:

```
results.txt
```

Useful for documentation and reports.

---

# 16. Save Results in XML

```bash
nmap -oX results.xml 192.168.1.1
```

### What it does

Exports results in XML format.

Useful for:

* Automation
* Parsing
* Security tools integration

---

# 17. Run Default NSE Scripts

```bash
nmap -sC 192.168.1.1
```

### What it does

Runs Nmap Scripting Engine default scripts.

### Information obtained

* Additional service information
* SSL details
* SMB information
* Login banners

---

# 18. Discover Service Banners

```bash
nmap -sV --script=banner 192.168.1.1
```

### What it does

Attempts to grab service banners.

### Information obtained

* Application names
* Version information
* Custom server banners

---

# 19. Vulnerability Detection Scripts

```bash
nmap --script vuln 192.168.1.1
```

### What it does

Runs vulnerability detection scripts.

### Information obtained

* Potential vulnerabilities
* Misconfigurations
* Weak services

⚠️ Only use on systems you own or have permission to test.

---

# 20. Comprehensive Recon Scan

```bash
sudo nmap -sS -sV -O -A -p- 192.168.1.1
```

### What it does

Performs a deep reconnaissance scan.

### Information obtained

* All open ports
* Service versions
* Operating system
* Traceroute
* Script results

This is often used during lab environments and authorized security assessments.

---

# Port States Explained

| State           | Meaning                                     |
| --------------- | ------------------------------------------- |
| open            | Service is accepting connections            |
| closed          | Port is reachable but no service is running |
| filtered        | Firewall is blocking detection              |
| unfiltered      | Accessible but state unknown                |
| open|filtered   | Nmap cannot determine which                 |
| closed|filtered | Nmap cannot determine which                 |

---

# Commonly Found Ports

| Port | Service        |
| ---- | -------------- |
| 21   | FTP            |
| 22   | SSH            |
| 23   | Telnet         |
| 25   | SMTP           |
| 53   | DNS            |
| 80   | HTTP           |
| 110  | POP3           |
| 143  | IMAP           |
| 443  | HTTPS          |
| 3306 | MySQL          |
| 3389 | RDP            |
| 5432 | PostgreSQL     |
| 8080 | HTTP Alternate |

---

## Final Note

Nmap is a reconnaissance and network administration tool. Always scan systems that you own or have explicit permission to test. Unauthorized scanning may violate laws, policies, or terms of service.

# Week 1 — Network Discovery Techniques
**Role 2 (Technical Lead) — Deliverable**
> Status: ✅ Complete | Week: 1 | Author: Role 2

---

## 1. What is Network Discovery?

Network discovery is the process of identifying active devices, open ports, running services, and potential vulnerabilities within a network. Attackers use these techniques during the **reconnaissance phase** of an attack. Understanding them is essential for defenders to know what an attacker sees.

---

## 2. Core Network Discovery Techniques

### 2.1 Ping Sweep (Host Discovery)
A ping sweep sends ICMP Echo Requests to a range of IP addresses to identify which hosts are alive on the network.

**How it works:**
- Attacker sends ICMP packets to an IP range (e.g., 192.168.1.1 – 192.168.1.254)
- Hosts that respond are considered "alive"
- Hosts that don't respond may have ICMP blocked or be offline

**Example using Nmap:**
```bash
nmap -sn 192.168.1.0/24
```

**Defensive countermeasure:** Block ICMP at the firewall perimeter to reduce visibility.

---

### 2.2 Port Scanning
Port scanning identifies which TCP/UDP ports are open on a target host. Open ports reveal running services.

**Types of port scans:**

| Scan Type | Description | Nmap Flag |
|-----------|-------------|-----------|
| TCP Connect | Full 3-way handshake, easily logged | `-sT` |
| SYN Scan (Stealth) | Half-open scan, harder to detect | `-sS` |
| UDP Scan | Scans UDP ports (slower) | `-sU` |
| NULL Scan | Sends packets with no flags set | `-sN` |
| FIN Scan | Sends FIN flag only | `-sF` |

**Example — Scan top 1000 ports:**
```bash
nmap -sS 192.168.1.10
```

**Example — Scan all 65535 ports:**
```bash
nmap -sS -p- 192.168.1.10
```

**Defensive countermeasure:** Close all unused ports. Use a firewall to whitelist only required services.

---

### 2.3 Service and Version Detection
Once open ports are found, attackers identify what software is running and its version to look for known vulnerabilities (CVEs).

**Example:**
```bash
nmap -sV 192.168.1.10
```

**Sample output:**
```
PORT    STATE SERVICE VERSION
22/tcp  open  ssh     OpenSSH 7.4 (protocol 2.0)
80/tcp  open  http    Apache httpd 2.4.6
3306/tcp open mysql   MySQL 5.7.28
```

**Why it matters:** MySQL 5.7.28 has known CVEs. An attacker now knows exactly what exploit to use.

**Defensive countermeasure:** Keep all services updated. Never run services on default ports when possible.

---

### 2.4 OS Detection
Attackers fingerprint the operating system of a target to tailor their attacks.

**Example:**
```bash
nmap -O 192.168.1.10
```

**Techniques used:**
- TTL (Time to Live) values in packets
- TCP window sizes
- Response to malformed packets

**Defensive countermeasure:** Use firewall rules to normalize TCP/IP responses and hide OS fingerprints.

---

### 2.5 Network Enumeration
Enumeration goes deeper than scanning — it extracts detailed information such as:
- Usernames and group names
- Network shares
- Routing tables
- SNMP community strings
- DNS zone transfers

**Common enumeration tools:**

| Tool | Purpose |
|------|---------|
| `enum4linux` | Enumerate Windows/Samba systems |
| `snmpwalk` | Extract SNMP data |
| `dig` / `nslookup` | DNS enumeration |
| `nbtscan` | NetBIOS scanning |

**Example — DNS zone transfer attempt:**
```bash
dig axfr @nameserver.target.com target.com
```

**Defensive countermeasure:** Disable zone transfers. Restrict SNMP community strings. Disable NetBIOS where not needed.

---

### 2.6 Full Nmap Reconnaissance Scan
A combined scan used by attackers for full initial reconnaissance:

```bash
nmap -sS -sV -O -A --script=default 192.168.1.0/24
```

**Flags explained:**
- `-sS` — SYN stealth scan
- `-sV` — Service version detection
- `-O` — OS detection
- `-A` — Aggressive scan (OS, version, scripts, traceroute)
- `--script=default` — Run default NSE scripts

---

## 3. Key Takeaways for Defenders

| Threat | Defense |
|--------|---------|
| Ping sweep reveals live hosts | Block ICMP at perimeter |
| Port scan reveals open services | Close unused ports, use firewall |
| Version scan reveals vulnerabilities | Patch all services regularly |
| OS fingerprinting aids exploitation | Normalize packet responses |
| Enumeration extracts user/share data | Restrict SNMP, DNS, NetBIOS |

---

## 4. References
- NIST SP 800-115: Technical Guide to Information Security Testing
- Nmap Official Documentation: https://nmap.org/docs.html
- SANS Institute: Network Reconnaissance Techniques
- CVE Database: https://cve.mitre.org

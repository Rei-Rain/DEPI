# Incident Scenario — Phishing-Led Ransomware Attack
**Cybersecurity Incident Response Framework — Week 3**
> Author: Role 1 (Research Lead) | Reviewed by: Role 2 (Technical Lead)

---

## Scenario Overview

| Field | Detail |
|-------|--------|
| Scenario Name | Operation Locked Vault |
| Attack Type | Phishing → Credential Theft → Lateral Movement → Ransomware |
| Simulated Date | Week 3, Day 1 |
| Affected Organization | TechCorp Ltd (simulated) |
| Industry | Financial Services |
| Severity Level | Critical |

---

## 1. Background

TechCorp Ltd is a mid-sized financial services company with 200 employees across two offices. The company manages client investment portfolios and stores sensitive financial data on internal servers. The IT team consists of 4 people and currently has no dedicated SOC (Security Operations Center).

---

## 2. Attack Vector and Timeline

### Stage 1 — Initial Access (Day 1, 09:14)
An employee in the Finance department receives a convincing spear-phishing email appearing to come from the company's HR department with the subject line: **"Urgent: Updated Benefits Enrollment — Action Required"**

The email contains a link to a fake Microsoft 365 login page hosted on a typosquatted domain (`microsofft-login.com`). The employee enters their credentials.

- **Attack type:** Spear phishing with credential harvesting
- **Compromised account:** `jsmith@techcorp.com` (Finance Analyst)
- **Attacker gains:** Valid Active Directory credentials

### Stage 2 — Persistence (Day 1, 09:31)
Using the stolen credentials, the attacker logs into the company VPN. They install a Remote Access Trojan (RAT) disguised as a software update pushed via the compromised account.

- **Tool used:** Custom RAT dropped via PowerShell
- **Persistence mechanism:** Scheduled task set to run at every login
- **Detection risk:** LOW — disguised as legitimate Windows update process

### Stage 3 — Reconnaissance (Day 1, 10:05)
From inside the network, the attacker performs internal network discovery:

```bash
# Commands simulated by attacker
nmap -sS -sV 192.168.10.0/24        # Scan User LAN
nmap -sS -sV 192.168.30.0/24        # Scan Server Zone
net user /domain                     # Enumerate domain users
net group "Domain Admins" /domain    # Identify admin accounts
```

- **Findings:** File server at 192.168.30.10, DB server at 192.168.30.20
- **High-value target identified:** File server containing financial records

### Stage 4 — Privilege Escalation (Day 1, 11:22)
The attacker exploits an unpatched local privilege escalation vulnerability (CVE-2021-34527 — PrintNightmare) on the Finance workstation to gain SYSTEM-level access.

- **CVE exploited:** CVE-2021-34527 (PrintNightmare — Windows Print Spooler)
- **Result:** Full SYSTEM privileges on compromised workstation
- **New capability:** Can now move to other systems using pass-the-hash

### Stage 5 — Lateral Movement (Day 1, 12:47)
Using stolen NTLM hashes, the attacker moves laterally to the file server using Pass-the-Hash attack.

- **Technique:** Pass-the-Hash (MITRE ATT&CK T1550.002)
- **Systems reached:** File server (192.168.30.10)
- **Access gained:** Full administrative access to file server

### Stage 6 — Data Exfiltration (Day 1, 14:10)
Before deploying ransomware, the attacker exfiltrates 2.3GB of sensitive financial records to an external server (attacker-controlled C2 at 185.220.101.x).

- **Data stolen:** Client financial records, investment portfolios, employee PII
- **Transfer method:** HTTPS to external IP over port 443 (blends with normal traffic)
- **Detection:** Possible via DLP or unusual outbound volume alerts

### Stage 7 — Ransomware Deployment (Day 1, 15:33)
The attacker deploys ransomware across all accessible shares on the file server and mapped network drives.

- **Ransomware variant:** LockBit 3.0 (simulated)
- **Files encrypted:** All .docx, .xlsx, .pdf, .csv files on the file server
- **Ransom note dropped:** `READ_ME_LOCKBIT.txt` on every encrypted directory
- **Ransom demand:** $50,000 in Bitcoin within 72 hours

### Stage 8 — Discovery by Victim (Day 1, 15:41)
An employee attempts to open a financial report and gets an error. They notify the IT helpdesk. Within minutes, multiple employees report they cannot access files. The IT team identifies encrypted files and the ransom note.

---

## 3. Expected Impact

| Category | Impact |
|----------|--------|
| Data Confidentiality | BREACHED — 2.3GB of client data exfiltrated |
| Data Integrity | COMPROMISED — Financial records encrypted |
| Availability | CRITICAL — File server inaccessible |
| Financial | Potential $50,000 ransom + regulatory fines |
| Reputational | High — client PII exposed |
| Regulatory | GDPR / financial data regulations triggered |

---

## 4. Systems Affected

| System | IP Address | Impact |
|--------|-----------|--------|
| Finance workstation | 192.168.10.45 | Initial compromise point |
| File server | 192.168.30.10 | Ransomware deployed, files encrypted |
| Domain Controller | 192.168.30.5 | Credential exposure (hashes stolen) |
| VPN Gateway | 192.168.1.1 | Used as entry point |

---

## 5. Indicators of Compromise (IOCs)

| Type | Value | Description |
|------|-------|-------------|
| Domain | microsofft-login.com | Phishing domain |
| IP | 185.220.101.x | Attacker C2 server |
| File hash | a3f8c2d1... (SHA-256) | RAT installer |
| Registry key | HKCU\Software\Microsoft\Windows\CurrentVersion\Run\UpdateSvc | Persistence mechanism |
| File | READ_ME_LOCKBIT.txt | Ransomware note |
| Process | powershell.exe -enc [base64] | Malicious PowerShell execution |

---

## 6. Simulation Instructions for Role 2

When executing the simulation (tabletop format):
1. Walk through each stage using this document as the script
2. At each stage, state out loud what the attacker has done
3. Role 3 documents all response actions taken at each stage
4. Apply the Week 2 IR Plan at each stage — detect, contain, eradicate, recover
5. Log timestamps for every action taken by the response team
6. Identify which controls from the hardening checklist would have prevented each stage

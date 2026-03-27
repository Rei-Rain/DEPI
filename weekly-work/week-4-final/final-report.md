# Final Report — Cybersecurity Incident Response Framework
**Comprehensive 4-Week Academic Project**
> Compiled by: Role 3 (Documentation Lead)
> Executive Summary: Role 1 | Technical Sections: Role 2 | Review: All members

---

## Table of Contents
1. Executive Summary
2. Introduction
3. Week 1 — Foundation and Awareness
4. Week 2 — Incident Response Planning
5. Week 3 — Simulated Incident and Response
6. Outcomes and Analysis
7. Lessons Learned and Recommendations
8. Conclusion
9. References

---

## 1. Executive Summary

This report presents the complete findings of a four-week cybersecurity incident response framework project conducted as part of an academic program. The project objective was to develop a comprehensive, end-to-end incident response capability covering research, planning, simulation, and review.

**Week 1** established the foundational knowledge base covering core cybersecurity principles, common threat types, and network discovery techniques used by attackers. The CIA Triad, Defense in Depth, and Zero Trust were identified as the guiding frameworks for all security decisions.

**Week 2** produced a formal Incident Response Plan aligned with NIST SP 800-61 and the SANS PICERL model. A secure network architecture was designed with five segmented zones, and a 40+ item system hardening checklist was developed covering operating systems, network devices, password policy, patch management, and encryption standards.

**Week 3** executed a full tabletop simulation of a phishing-led ransomware attack (Operation Locked Vault). The simulated attack progressed through eight stages over six hours. The IR team detected the incident within 8 minutes of ransomware deployment, achieved full containment in 32 minutes, completed eradication in 2 hours 15 minutes, and restored all systems within 3 hours 30 minutes. No ransom was paid.

**Key outcomes:** The IR Plan performed effectively under simulation. Six critical security gaps were identified and prioritized for remediation. The most critical finding was the absence of Multi-Factor Authentication on the VPN, which allowed the attacker to access the internal network using only a stolen password.

---

## 2. Introduction

### 2.1 Background

Cybersecurity incidents are increasing in frequency and sophistication. Ransomware attacks rose by 93% in 2021, with the average cost of a data breach reaching $4.45 million in 2023 (IBM Cost of a Data Breach Report). Organizations without a formal Incident Response Plan take an average of 298 days to identify and contain a breach — compared to 197 days for organizations with a mature IR capability.

This project was designed to address that gap by building a complete, practical IR framework from scratch over four weeks, culminating in a live simulation that tested the framework under realistic attack conditions.

### 2.2 Project Objectives
- Research and document the cybersecurity threat landscape
- Design a secure network architecture with defense-in-depth controls
- Develop a formal Incident Response Plan based on NIST and SANS standards
- Execute a realistic incident simulation and apply the IR Plan
- Identify gaps and produce actionable recommendations

### 2.3 Team Structure

| Role | Responsibility |
|------|---------------|
| Role 1 — Research Lead | Threat research, framework analysis, executive summary |
| Role 2 — Technical Lead | Architecture design, simulation execution, technical reporting |
| Role 3 — Documentation Lead | Report writing, compilation, document quality |
| Role 4 — Presenter Lead | Slides, speaker notes, presentation delivery |

---

## 3. Week 1 — Foundation and Awareness

### 3.1 Core Security Principles

The project established three foundational models governing all security decisions:

**CIA Triad:** Every security control must protect Confidentiality (data accessible only to authorized users), Integrity (data accuracy and tamper-evidence), and Availability (systems accessible when needed).

**Defense in Depth:** Security is implemented in layers — physical, network, host, application, and data. If one layer fails, the next provides protection.

**Zero Trust:** No user or device is trusted by default, even inside the network. Every access request must be authenticated and authorized.

### 3.2 Threat Landscape

The research identified six primary threat categories relevant to the simulated organization:

| Threat | Attack Method | Key Stat |
|--------|--------------|---------|
| Phishing | Social engineering via email | 80%+ of all incidents begin with phishing |
| Ransomware | Encrypt and extort | Up 93% in 2021, avg demand $812K |
| Malware | Trojans, worms, rootkits | Present in 94% of data breaches |
| DDoS | Traffic flood | Average attack costs $218K/hour downtime |
| Insider Threat | Abuse of legitimate access | 34% of all breaches involve insiders |
| Man-in-the-Middle | Intercept communications | Common in unprotected Wi-Fi environments |

### 3.3 Network Discovery Techniques

Understanding attacker reconnaissance is essential for defenders. Key techniques documented:

- **Ping sweep** (nmap -sn) — identifies live hosts on a network
- **Port scanning** (nmap -sS) — identifies open services
- **Service version detection** (nmap -sV) — identifies software versions and known CVEs
- **OS fingerprinting** (nmap -O) — enables OS-specific attack selection
- **Network enumeration** (enum4linux, snmpwalk) — extracts usernames, shares, and DNS data

**Defensive implication:** Every technique an attacker uses in reconnaissance maps to a specific hardening control — closing ports, blocking ICMP, restricting SNMP, disabling unnecessary services.

---

## 4. Week 2 — Incident Response Planning

### 4.1 IR Framework Adopted

The IR Plan combines two established frameworks:

**NIST SP 800-61 (4 phases):**
```
Preparation → Detection & Analysis → Containment, Eradication & Recovery → Post-Incident
```

**SANS PICERL (6 steps):**
```
Preparation → Identification → Containment → Eradication → Recovery → Lessons Learned
```

The combined six-phase approach provides both the structure of NIST and the operational granularity of SANS.

### 4.2 Secure Network Architecture

A five-zone segmented architecture was designed:

| Zone | VLAN | Purpose | Trust Level |
|------|------|---------|-------------|
| DMZ | 20 | Public-facing web and DNS servers | Untrusted |
| User LAN | 10 | Employee workstations | Low |
| Server Zone | 30 | Application, database, file servers | Medium |
| Management | 99 | SIEM, IDS, admin tools | High |
| VPN | 50 | Remote access — verified users only | Verified |

Key design principles:
- No direct DMZ-to-Server Zone communication
- Database accessible only from application server
- Management Zone accessible via MFA + VPN only
- All inter-zone traffic logged to SIEM

### 4.3 System Hardening — Key Controls

The hardening checklist covered five domains:

**Operating System:** Disable SMBv1, enable BitLocker, enforce account lockout (5 attempts/30 min), enable audit logging, remove default accounts.

**Network:** VLAN segmentation, disable Telnet (SSH only), enable DHCP snooping and Dynamic ARP Inspection, disable unused switch ports.

**Password Policy:** 12-character minimum, complexity required, 90-day rotation, 12-password history, MFA on all admin and remote access.

**Patch Management:** Critical patches (CVSS 9-10) within 48 hours, High within 7 days, Medium within 30 days.

**Encryption:** TLS 1.2+ only, AES-256 for data at rest, disable SSL 2.0/3.0 and weak cipher suites.

### 4.4 Access Control

**RBAC** was defined with five roles: Administrator, Security Analyst, Developer, End User, and Service Accounts — each with minimum required permissions.

**MFA** was mandated for all VPN access, administrator consoles, remote email, and cloud services.

---

## 5. Week 3 — Simulated Incident and Response

### 5.1 Scenario Summary — Operation Locked Vault

A phishing-led ransomware attack was simulated against TechCorp Ltd (financial services, 200 employees). The attack followed eight stages over a six-hour window:

| Stage | Time | Event |
|-------|------|-------|
| 1 | 09:14 | Spear phishing → credentials stolen |
| 2 | 09:31 | RAT installed via PowerShell |
| 3 | 10:05 | Internal network reconnaissance |
| 4 | 11:22 | PrintNightmare privilege escalation |
| 5 | 12:47 | Lateral movement via Pass-the-Hash |
| 6 | 14:10 | 2.3GB data exfiltrated |
| 7 | 15:33 | LockBit 3.0 ransomware deployed |
| 8 | 15:41 | Employee discovery — IR activated |

### 5.2 Response Performance

| Phase | Time Taken | Target | Result |
|-------|-----------|--------|--------|
| Detection | 8 minutes | < 15 min | ✅ MET |
| Containment | 32 minutes | < 60 min | ✅ MET |
| Eradication | 1 hour 45 min | < 4 hours | ✅ MET |
| Recovery | 1 hour 15 min | < 4 hours | ✅ MET |
| Total | 3 hours 30 min | < 8 hours | ✅ MET |

### 5.3 MITRE ATT&CK Coverage

All seven attack techniques were successfully identified and responded to:
T1566.002 (Phishing), T1053.005 (Persistence), T1046 (Discovery), T1068 (Privilege Escalation), T1550.002 (Lateral Movement), T1041 (Exfiltration), T1486 (Ransomware).

---

## 6. Outcomes and Analysis

### 6.1 IR Plan Effectiveness

The Week 2 IR Plan was followed precisely during the simulation without improvisation. All six phases executed in order. The plan proved:
- **Practical** — actions were specific enough to execute in real time
- **Complete** — no phase was missing or unclear
- **Effective** — all response objectives were met within target times

### 6.2 Security Architecture Effectiveness

The segmented network architecture limited the blast radius of the attack:
- Ransomware reached only the file server — the database and application server were not compromised
- Management Zone was not reached — SIEM and admin tools remained operational throughout
- The attack was stopped at the Server Zone boundary

**What the architecture did not prevent:** The initial phishing entry and the VPN-based access because MFA was not enforced.

### 6.3 Key Metrics

| Metric | Value |
|--------|-------|
| Systems compromised | 2 workstations + 1 file server |
| Systems that could have been compromised (without segmentation) | All 47 endpoints + 3 servers |
| Data exfiltrated | 2.3 GB |
| Data lost (unrecoverable) | ~12 files (same-day activity) |
| Recovery from backup | 100% |
| Ransom paid | $0 |
| Estimated cost avoided by not paying ransom | $50,000 |

---

## 7. Lessons Learned and Recommendations

### 7.1 Critical Findings

| Priority | Gap | Impact | Recommendation |
|----------|-----|--------|---------------|
| CRITICAL | No MFA on VPN | Attacker accessed network with only a stolen password | Enforce MFA on all VPN immediately |
| HIGH | PrintNightmare unpatched 6 months | Enabled full privilege escalation | Enforce 48-hour critical patch SLA |
| HIGH | No DLP solution | 2.3GB exfiltrated undetected | Deploy Data Loss Prevention |
| HIGH | No advanced email filtering | Phishing email delivered successfully | Deploy Defender for Office 365 |
| MEDIUM | No EDR on all endpoints | Second infected workstation found late | Roll out EDR to all 200 endpoints |
| MEDIUM | Daily backups only | Lost same-day file activity | Move to hourly incremental backups |

### 7.2 What the Framework Got Right

- Comprehensive pre-incident preparation through the hardening checklist
- Clear severity classification enabling rapid Critical-level response
- Network segmentation significantly limited lateral spread
- Evidence preservation procedures protected forensic integrity
- Clean backup availability enabled full recovery without paying ransom

### 7.3 Framework Improvements for Next Version

1. Add a **DLP monitoring** section to Phase 2 (Detection)
2. Add **MFA enforcement** as a mandatory Preparation checklist item
3. Add **EDR deployment** as a required tool in the tools inventory
4. Add **hourly backup verification** to the Recovery phase checklist
5. Add a **GDPR/regulatory notification** procedure to post-incident activities

---

## 8. Conclusion

This project successfully achieved all four objectives. A complete cybersecurity incident response framework was built from foundational research through live simulation, producing:

- A research report documenting the threat landscape and attacker techniques
- A formal IR Plan aligned with NIST and SANS standards
- A secure network architecture with five-zone segmentation
- A 40+ item system hardening checklist
- A full tabletop simulation with timestamped response log
- Six prioritized recommendations for improving the security posture

The simulation demonstrated that a structured IR Plan significantly reduces response time and prevents escalation. The team detected and contained a critical ransomware attack in under 32 minutes, restored all systems within 3.5 hours, and avoided a $50,000 ransom payment.

The most important finding of this project is that technical controls alone are insufficient. The attack succeeded initially because of a missing procedural control — Multi-Factor Authentication on VPN — not because of a failure in the technical architecture. This underscores the principle that people, process, and technology must all be addressed for a security program to be effective.

---

## 9. References

1. NIST SP 800-61 Rev. 2 — Computer Security Incident Handling Guide
2. SANS Institute — Incident Handler's Handbook
3. MITRE ATT&CK Framework — https://attack.mitre.org
4. CIS Controls v8 — https://www.cisecurity.org
5. ISO/IEC 27035 — Information Security Incident Management
6. IBM Cost of a Data Breach Report 2023
7. Verizon Data Breach Investigations Report (DBIR) 2023
8. CVE-2021-34527 — PrintNightmare — https://cve.mitre.org
9. DISA STIGs — https://public.cyber.mil/stigs
10. CIS Benchmarks — https://www.cisecurity.org/cis-benchmarks

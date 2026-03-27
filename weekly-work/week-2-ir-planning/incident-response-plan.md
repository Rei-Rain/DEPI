# Incident Response Plan
**Cybersecurity Incident Response Framework — Week 2**
> Status: Complete | Author: Role 3 | Technical Input: Role 2 | Framework Research: Role 1

---

## Table of Contents
1. Scope and Purpose
2. Roles and Responsibilities
3. IR Framework Reference (NIST + SANS)
4. Phase 1 — Preparation
5. Phase 2 — Detection and Analysis
6. Phase 3 — Containment
7. Phase 4 — Eradication
8. Phase 5 — Recovery
9. Phase 6 — Lessons Learned
10. Access Control Measures
11. References

---

## 1. Scope and Purpose

### Purpose
This Incident Response (IR) Plan defines the procedures the organization follows when a cybersecurity incident is detected. It ensures a structured, repeatable, and documented response that minimizes damage, reduces recovery time, and prevents recurrence.

### Scope
This plan applies to:
- All information systems, networks, and data assets
- All employees, contractors, and third-party users with system access
- All incident types including malware, unauthorized access, data breaches, DDoS, and insider threats

### Activation Criteria
This plan is activated when any of the following are confirmed or suspected:
- Unauthorized access to systems or data
- Malware infection or ransomware deployment
- Data exfiltration or breach
- Significant service disruption
- Insider threat activity

---

## 2. Roles and Responsibilities

| Role | Responsibility |
|------|---------------|
| Incident Response Lead | Coordinates the entire IR process, makes escalation decisions |
| Technical Analyst (Role 2) | Executes technical investigation, containment, and eradication |
| Documentation Specialist (Role 3) | Records all actions, timestamps, and outcomes |
| Communications Lead (Role 4) | Manages internal/external communication and reporting |
| Research Analyst (Role 1) | Provides threat intelligence and framework guidance |

---

## 3. IR Framework Reference

### 3.1 NIST SP 800-61 — Four Phases
The NIST framework defines incident response in four phases:

```
Preparation → Detection & Analysis → Containment, Eradication & Recovery → Post-Incident Activity
```

### 3.2 SANS — Six-Step IR Model (PICERL)
The SANS model expands to six steps:

```
Preparation → Identification → Containment → Eradication → Recovery → Lessons Learned
```

### Combined Approach Used in This Plan
This IR plan combines both frameworks into six actionable phases for maximum coverage.

---

## 4. Phase 1 — Preparation

**Objective:** Establish the tools, policies, and capabilities needed to respond effectively before an incident occurs.

### 4.1 Asset Inventory
- Maintain an up-to-date inventory of all hardware, software, and data assets
- Classify assets by criticality (Critical / High / Medium / Low)
- Document all network segments and access points

### 4.2 Security Policies Required
- Acceptable Use Policy (AUP)
- Password and Authentication Policy
- Data Classification Policy
- Remote Access Policy
- Incident Reporting Policy

### 4.3 Tools and Infrastructure
| Tool Category | Examples |
|---------------|---------|
| SIEM (Log aggregation) | Splunk, IBM QRadar, Microsoft Sentinel |
| IDS/IPS | Snort, Suricata |
| Endpoint Detection | CrowdStrike, SentinelOne |
| Network Monitor | Wireshark, Zeek |
| Forensic Tools | Volatility, Autopsy, FTK |
| Communication | Secure out-of-band channel (Signal, encrypted email) |

### 4.4 Team Readiness
- All IR team members trained on this plan
- Contact list for all stakeholders maintained and updated
- IR exercises (tabletop simulations) conducted regularly

---

## 5. Phase 2 — Detection and Analysis

**Objective:** Identify that an incident has occurred, determine its scope, and classify its severity.

### 5.1 Detection Sources
- SIEM alerts and log analysis
- IDS/IPS alerts
- User reports (helpdesk tickets)
- Automated vulnerability scanners
- Threat intelligence feeds

### 5.2 Initial Analysis Checklist
- [ ] Confirm the alert is not a false positive
- [ ] Identify affected systems, accounts, and data
- [ ] Determine attack vector (how did they get in?)
- [ ] Establish a timeline of events
- [ ] Classify incident severity

### 5.3 Severity Classification

| Level | Description | Response Time |
|-------|-------------|---------------|
| Critical | Data breach, ransomware, full system compromise | Immediate (< 1 hour) |
| High | Unauthorized access, active malware spread | < 4 hours |
| Medium | Isolated malware, policy violation | < 24 hours |
| Low | Suspicious activity, minor policy breach | < 72 hours |

### 5.4 Evidence Collection
- Capture system memory (RAM) before shutdown
- Preserve system logs with timestamps
- Hash all collected files (MD5/SHA-256) to prove integrity
- Document chain of custody for all evidence

---

## 6. Phase 3 — Containment

**Objective:** Stop the spread of the incident and limit damage without destroying evidence.

### 6.1 Short-Term Containment (Immediate)
- Isolate affected systems from the network (disconnect but do not power off)
- Block attacker IP addresses at the firewall
- Disable compromised user accounts
- Preserve system state for forensic analysis

### 6.2 Long-Term Containment
- Apply emergency patches to vulnerable systems
- Implement additional monitoring on adjacent systems
- Deploy honeypots to monitor attacker movement
- Enforce stricter access controls on sensitive data

### 6.3 Containment Decision Matrix

| Incident Type | Containment Action |
|--------------|-------------------|
| Malware infection | Network isolation of affected host |
| Ransomware | Immediate isolation + snapshot of encrypted files |
| Unauthorized access | Disable account + revoke active sessions |
| DDoS | Enable rate limiting + contact ISP for upstream filtering |
| Insider threat | Suspend access + preserve all activity logs |
| Data exfiltration | Block outbound connections + identify exfil destination |

---

## 7. Phase 4 — Eradication

**Objective:** Remove the threat completely from the environment.

### 7.1 Eradication Steps
1. Identify root cause — how did the attacker initially gain access?
2. Remove all malware, backdoors, and unauthorized accounts
3. Delete attacker-created files, scheduled tasks, and registry keys
4. Patch the vulnerability that was exploited
5. Reset all potentially compromised credentials
6. Scan all systems in the same network segment

### 7.2 Validation
- Run full antivirus/EDR scan on all systems in scope
- Review all user accounts — remove any unauthorized accounts
- Confirm all patches have been successfully applied
- Verify no persistent backdoors remain (check startup items, cron jobs, scheduled tasks)

---

## 8. Phase 5 — Recovery

**Objective:** Restore affected systems to normal operation safely and verify integrity.

### 8.1 Recovery Steps
1. Restore systems from clean, verified backups (check backup dates vs. intrusion date)
2. Rebuild compromised systems from scratch if backup integrity is uncertain
3. Reset all passwords for affected users and service accounts
4. Re-enable systems gradually — monitor closely before full restoration
5. Verify system integrity with hash verification of critical files
6. Confirm normal business operations have resumed

### 8.2 Return-to-Operations Checklist
- [ ] All malware confirmed removed
- [ ] All patches applied
- [ ] All compromised credentials reset
- [ ] Systems restored from clean backup
- [ ] Enhanced monitoring active
- [ ] Stakeholders notified of resolution

---

## 9. Phase 6 — Lessons Learned

**Objective:** Improve future response by documenting what happened and what can be improved.

### 9.1 Post-Incident Review (Within 2 Weeks)
Conduct a structured review meeting covering:
- What happened and when?
- How was the incident detected?
- What worked well in the response?
- What did not work? Where were the gaps?
- What could have prevented this incident?

### 9.2 Documentation Required
- Full incident report (timeline, impact, response actions)
- Root cause analysis
- Updated IR plan (if procedures need revision)
- Training recommendations for staff

---

## 10. Access Control Measures

### 10.1 Role-Based Access Control (RBAC)
Assign permissions based on job role — not individual preferences.

| Role | Access Level |
|------|-------------|
| Administrator | Full system access (restricted to named individuals) |
| Developer | Development environment only |
| Analyst | Read access to logs and monitoring dashboards |
| End User | Access only to tools needed for their job |

### 10.2 Multi-Factor Authentication (MFA)
MFA must be enforced for:
- All remote access (VPN, RDP)
- All administrator accounts
- All cloud service logins
- Email access

### 10.3 Privileged Access Management (PAM)
- Privileged accounts are separate from regular accounts
- Privileged sessions are logged and recorded
- Just-in-time (JIT) access granted only when needed
- Regular review of all privileged account holders

---

## 11. References
1. NIST SP 800-61 Rev. 2 — Computer Security Incident Handling Guide
2. SANS Incident Handler's Handbook — https://www.sans.org
3. MITRE ATT&CK Framework — https://attack.mitre.org
4. CIS Controls v8 — https://www.cisecurity.org
5. ISO/IEC 27035 — Information Security Incident Management

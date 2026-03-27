# Incident Response Documentation
## Containment, Eradication, and Recovery Report
**Cybersecurity Incident Response Framework — Week 3**
> Author: Role 3 (Documentation Lead) | Input: All team members

---

## Executive Summary

On simulation day, TechCorp Ltd experienced a critical cybersecurity incident involving spear phishing, credential theft, lateral movement, data exfiltration, and ransomware deployment across the file server. The incident was detected at T+00:00, fully contained by T+00:32, eradicated by T+02:15, and systems restored by T+03:30. Total simulation response time: **3 hours 30 minutes**.

No ransom was paid. Systems were fully restored from clean backup. Two compromised workstations were cleaned and returned to service.

---

## 1. Incident Timeline Summary

| Time | Event |
|------|-------|
| T-06:19 (14:10) | Attacker begins data exfiltration (2.3GB) — undetected |
| T-00:08 (15:33) | Ransomware deployed on file server |
| T+00:00 (15:41) | Employee reports file access failure — IR activated |
| T+00:15 | Containment begins |
| T+00:32 | Containment complete — spread stopped |
| T+01:00 | Eradication begins |
| T+02:15 | Eradication complete — all threats removed |
| T+02:30 | Recovery begins |
| T+03:30 | Recovery complete — all systems operational |

---

## 2. Containment Report

### 2.1 Containment Objective
Stop the ransomware from spreading to additional systems while preserving forensic evidence for investigation.

### 2.2 Actions Taken

#### Network Isolation
- **192.168.10.45** (Finance workstation) — disconnected from network at T+00:15
- **192.168.30.10** (File server) — disconnected from network at T+00:17
- Network isolation performed by pulling logical network access (VLAN reassignment) — systems NOT powered off to preserve RAM state

#### Account Actions
- Compromised account **jsmith@techcorp.com** disabled at T+00:19
- All active VPN sessions for jsmith revoked
- Domain Admin password rotation initiated as precaution

#### Firewall and DNS Blocks
- Attacker C2 IP **185.220.101.x** blocked at perimeter firewall — T+00:21
- Phishing domain **microsofft-login.com** blocked at DNS resolver — T+00:23

#### Evidence Preservation
- Memory dump captured from file server at T+00:25 — hash: `SHA-256: b7f2a3c9...`
- Disk image of Finance workstation captured at T+00:27 — hash: `SHA-256: d4e8c1f7...`
- All images stored on isolated forensic workstation (not connected to network)

### 2.3 Containment Effectiveness Assessment

| Control | Effective? | Notes |
|---------|-----------|-------|
| Network isolation | YES | Spread stopped immediately |
| Account disabling | YES | Attacker lost remote access |
| C2 blocking | YES | Exfiltration channel closed |
| Evidence preservation | YES | Memory and disk images captured |
| Speed of containment | PARTIAL | 15 minutes from detection — target is under 10 minutes |

---

## 3. Eradication Report

### 3.1 Eradication Objective
Completely remove all attacker tools, backdoors, and persistence mechanisms. Patch the root cause vulnerability.

### 3.2 Root Cause Analysis

| Factor | Detail |
|--------|--------|
| Initial entry | Phishing email — employee clicked malicious link |
| Why it worked | No MFA on VPN — stolen password was sufficient for access |
| How attacker escalated | PrintNightmare (CVE-2021-34527) — unpatched for 6 months |
| How attacker moved laterally | Pass-the-Hash attack using stolen NTLM hashes |
| Why exfiltration was missed | No DLP solution — HTTPS outbound traffic not inspected |

### 3.3 Malware Removed

| System | Malware Found | Location | Removed |
|--------|--------------|---------|---------|
| 192.168.10.45 | RAT (UpdateSvc.exe) | C:\Windows\System32\ | YES |
| 192.168.10.45 | Scheduled task | Task Scheduler → UpdateSvc | YES |
| 192.168.10.45 | Registry persistence | HKCU\...\Run\UpdateSvc | YES |
| 192.168.10.52 | RAT (UpdateSvc.exe) | C:\Windows\System32\ | YES |
| File server | LockBit ransomware binary | C:\Windows\Temp\ | YES |

### 3.4 Credentials Reset

| Account | Reset | New MFA Enrolled |
|---------|-------|-----------------|
| jsmith@techcorp.com | YES | YES |
| All Domain Admin accounts (4) | YES | YES |
| File server service account | YES | N/A |
| VPN gateway service account | YES | N/A |

### 3.5 Patches Applied

| CVE | Severity | System | Patch Applied | Time |
|-----|---------|--------|--------------|------|
| CVE-2021-34527 (PrintNightmare) | Critical | All Windows hosts | YES | T+01:50 |
| Additional critical patches found during review | High | App server | YES | T+02:00 |

### 3.6 Eradication Validation
- Full Defender AV scan completed on all 47 endpoints — **2 infected, both cleaned**
- No additional persistence mechanisms found
- All startup items, scheduled tasks, cron jobs reviewed — clean
- Network traffic monitoring confirms no further C2 communication

---

## 4. Recovery Report

### 4.1 Recovery Objective
Restore all affected systems to verified clean state and return to normal business operations under enhanced monitoring.

### 4.2 Backup Integrity Verification

| System | Backup Date | Backup Hash Verified | Integrity Status |
|--------|------------|---------------------|-----------------|
| File server | Day -1 (00:00) | YES — SHA-256 matched | CLEAN |
| Finance workstation | Day -3 | YES — SHA-256 matched | CLEAN |

**Data Loss Assessment:** Files created or modified on the day of the incident are not recoverable from backup. Activity logs indicate normal working-day document activity — estimated 12 files created that day.

### 4.3 Recovery Actions

| Action | System | Time | Verified By |
|--------|--------|------|------------|
| Restore file server from backup | 192.168.30.10 | T+02:45 | Role 2 |
| Verify file integrity post-restore | 192.168.30.10 | T+03:10 | Role 2 |
| Reconnect file server with enhanced monitoring | 192.168.30.10 | T+03:00 | Role 2 |
| Rebuild Finance workstation from baseline | 192.168.10.45 | T+03:20 | Role 2 |
| Rebuild second compromised workstation | 192.168.10.52 | T+03:25 | Role 2 |
| Confirm all services operational | All systems | T+03:30 | IR Lead |

### 4.4 Enhanced Monitoring Applied Post-Recovery

- SIEM alert thresholds lowered by 50% for 72 hours
- All outbound traffic over 100MB flagged for manual review
- Privileged account activity monitored in real-time for 7 days
- Daily vulnerability scan scheduled for 30 days post-incident

---

## 5. Lessons Learned

### 5.1 What Worked Well

| Item | Detail |
|------|--------|
| Detection speed | Incident detected within 8 minutes of ransomware deployment |
| Evidence preservation | Memory and disk images captured before systems were cleaned |
| Team coordination | All 4 members executed their roles as planned |
| Backup restore | Clean backup available and fully restored in 45 minutes |
| IR Plan adherence | Week 2 IR Plan followed precisely — no improvisation needed |

### 5.2 What Did Not Work / Gaps Found

| Gap | Impact | Priority Fix |
|-----|--------|-------------|
| No MFA on VPN | Attacker accessed network with just a stolen password | CRITICAL — Fix immediately |
| PrintNightmare unpatched for 6 months | Enabled privilege escalation | HIGH — Enforce 48hr patch policy |
| No DLP solution | 2.3GB exfiltrated without detection | HIGH — Deploy DLP within 30 days |
| No anti-phishing email filter | Phishing email delivered successfully | HIGH — Deploy advanced email filtering |
| No EDR on all endpoints | Second infected workstation not found until T+01:25 | MEDIUM — Deploy EDR on all hosts |
| Hourly backups not in place | Lost one full day of file changes | MEDIUM — Move to hourly incremental backups |

### 5.3 Recommendations

1. **Enforce MFA on VPN immediately** — single highest-impact fix
2. **Deploy Microsoft Defender for Office 365** — blocks phishing before delivery
3. **Implement 48-hour critical patch policy** — PrintNightmare was patched by Microsoft 6 months prior
4. **Deploy DLP solution** — would have flagged 2.3GB outbound transfer
5. **Roll out EDR to all 200 endpoints** — full visibility across the estate
6. **Move to hourly incremental backups** — reduces data loss window from 24 hours to 1 hour
7. **Conduct quarterly tabletop exercises** — keeps the team sharp and the IR plan current

---

## 6. Incident Closure

| Field | Value |
|-------|-------|
| Incident Status | CLOSED |
| Ransom Paid | NO |
| Systems Restored | YES — all 3 affected systems |
| Data Loss | Minimal — same-day file activity only |
| Data Breach | YES — 2.3GB exfiltrated (regulatory notification required) |
| Regulatory Notification | Required under GDPR Article 33 within 72 hours |
| IR Plan Updates Required | YES — 6 updates identified (see Section 5.2) |
| Follow-up Review Date | 2 weeks post-incident |

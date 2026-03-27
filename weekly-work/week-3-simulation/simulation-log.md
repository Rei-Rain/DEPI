# Simulation Execution Log — Operation Locked Vault
**Cybersecurity Incident Response Framework — Week 3**
> Author: Role 2 (Technical Lead) | Documented by: Role 3
> All timestamps are simulation time. This is a tabletop exercise.

---

## Simulation Details

| Field | Value |
|-------|-------|
| Simulation Type | Tabletop Exercise |
| All Members Present | Yes — all 4 required |
| IR Plan Used | Week 2 Incident Response Plan |
| Scenario | Phishing → Ransomware (Operation Locked Vault) |

---

## Phase-by-Phase Response Log

---

### PHASE 1 — DETECTION
**Simulation Time: T+00:00**

| Time | Actor | Action Taken | Outcome |
|------|-------|-------------|---------|
| T+00:00 | End User | Employee reports cannot open financial files | Helpdesk ticket #1042 created |
| T+00:03 | IT Helpdesk | Checks file server — finds encrypted files and ransom note | Incident declared |
| T+00:05 | IR Lead | IR Plan activated — Severity: CRITICAL | All IR team members alerted |
| T+00:07 | Role 2 | Checks SIEM — identifies unusual outbound traffic spike at 14:10 | Possible data exfiltration confirmed |
| T+00:09 | Role 2 | Identifies source workstation: 192.168.10.45 (Finance Analyst) | Initial compromise point found |
| T+00:11 | Role 1 | Searches threat intelligence feeds — identifies IOCs matching LockBit 3.0 | Ransomware variant confirmed |

**Detection Finding:** Incident was detected 8 minutes after ransomware deployment. SIEM alert on outbound volume was the key technical indicator. User report was the first human signal.

---

### PHASE 2 — CONTAINMENT
**Simulation Time: T+00:15**

| Time | Actor | Action Taken | Outcome |
|------|-------|-------------|---------|
| T+00:15 | Role 2 | Isolates Finance workstation 192.168.10.45 from network | Attacker loses foothold on workstation |
| T+00:17 | Role 2 | Isolates file server 192.168.30.10 from network | Ransomware spread stopped |
| T+00:19 | IR Lead | Disables compromised user account jsmith@techcorp.com | Active sessions revoked |
| T+00:21 | Role 2 | Blocks attacker C2 IP 185.220.101.x at perimeter firewall | Outbound exfiltration channel closed |
| T+00:23 | Role 2 | Blocks phishing domain microsofft-login.com at DNS level | Prevents further credential harvesting |
| T+00:25 | Role 2 | Takes memory snapshot of file server before shutdown | Forensic evidence preserved |
| T+00:27 | Role 2 | Takes disk image of compromised workstation | Chain of custody maintained |
| T+00:30 | Role 3 | Logs all actions with timestamps into this document | Documentation complete |
| T+00:32 | Role 4 | Drafts internal communication to all employees about file outage | Employees informed without triggering panic |

**Containment Result:** Spread successfully stopped. Attacker access removed. Evidence preserved. 2 systems isolated. No additional systems reached.

---

### PHASE 3 — ERADICATION
**Simulation Time: T+01:00**

| Time | Actor | Action Taken | Outcome |
|------|-------|-------------|---------|
| T+01:00 | Role 2 | Performs forensic analysis on workstation memory dump | RAT identified: located at C:\Windows\System32\UpdateSvc.exe |
| T+01:15 | Role 2 | Identifies persistence mechanism: HKCU Run key for UpdateSvc | Scheduled task also found — both removed |
| T+01:25 | Role 2 | Full antivirus scan on all systems in same network segment | 1 additional workstation found with RAT (192.168.10.52) |
| T+01:30 | Role 2 | Isolates 192.168.10.52 — removes RAT — cleans system | Second compromised system cleaned |
| T+01:45 | Role 2 | Resets credentials: jsmith + all Domain Admin accounts | All potentially exposed credentials invalidated |
| T+01:50 | Role 2 | Applies patch for CVE-2021-34527 (PrintNightmare) on all systems | Root cause vulnerability patched |
| T+02:00 | Role 2 | Verifies no additional persistence mechanisms remain | All startup items, cron jobs, scheduled tasks reviewed — clean |
| T+02:10 | Role 1 | Cross-references IOCs with MITRE ATT&CK | Attack mapped: T1566.002, T1078, T1550.002, T1486 |
| T+02:15 | Role 3 | Documents complete eradication steps and findings | Eradication report section complete |

**Eradication Result:** Root cause identified and patched. All malware removed from 2 systems. All compromised credentials reset. No further backdoors found.

---

### PHASE 4 — RECOVERY
**Simulation Time: T+02:30**

| Time | Actor | Action Taken | Outcome |
|------|-------|-------------|---------|
| T+02:30 | Role 2 | Checks backup integrity — last clean backup dated Day-1 00:00 | Backup confirmed clean (pre-infection) |
| T+02:45 | Role 2 | Restores file server from clean backup | File server restored successfully |
| T+03:00 | Role 2 | Reconnects file server to network under enhanced monitoring | SIEM alert threshold lowered for 72 hours |
| T+03:10 | Role 2 | Verifies restored file hashes match backup hashes | Integrity confirmed — no tampering |
| T+03:20 | Role 2 | Restores Finance workstation from clean image | Workstation rebuilt from baseline |
| T+03:30 | IR Lead | Confirms all critical systems operational | Business operations restored |
| T+03:35 | Role 4 | Sends all-clear communication to employees | Employees notified of resolution |
| T+03:40 | Role 3 | Documents all recovery steps with timestamps | Recovery log complete |

**Recovery Result:** Full restoration from clean backup. Zero data lost from backup (loss window: same-day activity only). All systems operational under enhanced monitoring.

---

### PHASE 5 — POST-INCIDENT NOTES
**Simulation Time: T+04:00**

| Finding | Gap Identified | Recommendation |
|---------|----------------|----------------|
| Phishing email bypassed email filter | No advanced anti-phishing in place | Deploy Microsoft Defender for Office 365 |
| PrintNightmare unpatched for 6 months | Patch management process too slow | Enforce 48-hour critical patch policy |
| Exfiltration went undetected for 83 minutes | No DLP solution in place | Deploy Data Loss Prevention tool |
| No MFA on VPN | Allowed attacker in with only stolen password | Enforce MFA on all VPN access immediately |
| Backup restore took 45 minutes | Recovery objective could be tighter | Move to incremental hourly backups |
| Second compromised workstation not found until T+01:25 | Endpoint monitoring gaps | Deploy EDR on all endpoints |

---

## MITRE ATT&CK Mapping

| Tactic | Technique | ID | Used In Scenario |
|--------|-----------|-----|-----------------|
| Initial Access | Spear-Phishing Link | T1566.002 | Stage 1 — phishing email |
| Credential Access | Credentials from Web Browser | T1555.003 | Stage 1 — credential harvesting |
| Persistence | Scheduled Task/Job | T1053.005 | Stage 2 — RAT persistence |
| Discovery | Network Service Scan | T1046 | Stage 3 — Nmap scan |
| Privilege Escalation | Exploitation of Vulnerability | T1068 | Stage 4 — PrintNightmare |
| Lateral Movement | Pass the Hash | T1550.002 | Stage 5 — file server access |
| Exfiltration | Exfil Over C2 Channel | T1041 | Stage 6 — data theft |
| Impact | Data Encrypted for Impact | T1486 | Stage 7 — ransomware |

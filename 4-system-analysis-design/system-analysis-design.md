# System Analysis & Design
## Cybersecurity Incident Response Framework
**Document Type:** System Analysis & Design | **Section:** 4

---

## 1. Problem Statement & Objectives

### Problem Statement
Organizations face escalating cybersecurity threats but lack structured, tested, and documented incident response capabilities. Without a formal IR framework, incidents take longer to detect, contain, and recover from — resulting in higher financial losses, regulatory penalties, and reputational damage.

### Project Goals
1. Build a reusable IR Framework applicable to any mid-sized organization
2. Design a secure network architecture that limits attack blast radius
3. Validate the framework through realistic tabletop simulation
4. Produce complete documentation meeting DEPI academic standards

---

## 2. Use Case Diagram (Text Representation)

```
                    ┌─────────────────────────────────────────────┐
                    │         CYBERSECURITY IR SYSTEM             │
                    │                                             │
  [End User]  ──────┼──→ Report Suspicious Activity               │
                    │         │                                   │
  [Helpdesk]  ──────┼──→ Create Incident Ticket                   │
                    │         │                                   │
  [IR Lead]   ──────┼──→ Activate IR Plan                         │
                    │    ├──→ Classify Severity                   │
                    │    ├──→ Assign Response Team                │
                    │    └──→ Escalate to Management              │
                    │                                             │
  [Technical  ──────┼──→ Isolate Affected Systems                 │
   Analyst]         │    ├──→ Collect Forensic Evidence           │
                    │    ├──→ Eradicate Malware                   │
                    │    └──→ Restore from Backup                 │
                    │                                             │
  [Doc Lead]  ──────┼──→ Document All Response Actions            │
                    │    └──→ Produce Incident Report             │
                    │                                             │
  [Presenter] ──────┼──→ Communicate to Stakeholders              │
                    │    └──→ Deliver Final Presentation          │
                    │                                             │
  [SIEM]      ──────┼──→ Generate Automated Alerts                │
  [Firewall]  ──────┼──→ Block Attacker C2                        │
  [Backup]    ──────┼──→ Provide Clean Restore Point              │
                    └─────────────────────────────────────────────┘
```

---

## 3. Software Architecture

### Architecture Style: Layered Defense / Defense in Depth

```
┌──────────────────────────────────────────────────────────────────┐
│                     EXTERNAL LAYER                               │
│  Internet → Perimeter Firewall → DMZ (Web Server, DNS)          │
└──────────────────────────┬───────────────────────────────────────┘
                           │ Filtered traffic only
┌──────────────────────────▼───────────────────────────────────────┐
│                    NETWORK LAYER                                  │
│  WAF + IDS/IPS → Internal Firewall → VLAN Segmentation          │
│  User LAN (VLAN 10) | Server Zone (VLAN 30) | Mgmt (VLAN 99)   │
└──────────────────────────┬───────────────────────────────────────┘
                           │ Authenticated access only
┌──────────────────────────▼───────────────────────────────────────┐
│                  APPLICATION LAYER                                │
│  App Server → Database Server → File Server                      │
│  RBAC enforced | MFA required | All sessions logged             │
└──────────────────────────┬───────────────────────────────────────┘
                           │ Encrypted (AES-256 / TLS 1.2+)
┌──────────────────────────▼───────────────────────────────────────┐
│                     DATA LAYER                                    │
│  Encrypted storage | Daily + Incremental backups | Hash verified │
└──────────────────────────────────────────────────────────────────┘
```

**Architecture Pattern:** Layered (N-tier) with VLAN segmentation
**Security Model:** Zero Trust — no implicit trust between zones
**Access Control:** RBAC with MFA enforcement at zone boundaries

---

## 4. Database Design & Data Modeling

### 4.1 ER Diagram (Entity-Relationship)

```
┌────────────┐        ┌──────────────┐        ┌──────────────┐
│  INCIDENT  │        │   RESPONSE   │        │    ASSET     │
│────────────│        │──────────────│        │──────────────│
│ incident_id│◄──────►│ response_id  │        │ asset_id     │
│ date_time  │  1:M   │ incident_id  │        │ asset_name   │
│ severity   │        │ action_taken │        │ ip_address   │
│ type       │        │ actor        │        │ asset_type   │
│ status     │        │ timestamp    │        │ criticality  │
│ description│        │ outcome      │        │ zone         │
└─────┬──────┘        └──────────────┘        └──────┬───────┘
      │                                               │
      │ M:M                                      M:M │
      ▼                                               ▼
┌────────────┐        ┌──────────────┐        ┌──────────────┐
│  AFFECTED  │        │     IOC      │        │    USER      │
│   ASSETS   │        │──────────────│        │──────────────│
│────────────│        │ ioc_id       │        │ user_id      │
│ incident_id│        │ incident_id  │        │ username     │
│ asset_id   │        │ ioc_type     │        │ role         │
│ impact     │        │ ioc_value    │        │ department   │
└────────────┘        │ date_found   │        │ access_level │
                      └──────────────┘        └──────────────┘
```

### 4.2 Logical Schema

**INCIDENT** (incident_id PK, date_time, severity ENUM, type, status ENUM, description, detected_by)
**RESPONSE** (response_id PK, incident_id FK, action_taken, actor_role, timestamp, outcome, phase ENUM)
**ASSET** (asset_id PK, asset_name, ip_address, asset_type, criticality ENUM, zone, os)
**AFFECTED_ASSETS** (incident_id FK, asset_id FK, impact_description) — Junction table
**IOC** (ioc_id PK, incident_id FK, ioc_type ENUM, ioc_value, date_found, source)
**USER** (user_id PK, username, role, department, access_level ENUM, mfa_enabled BOOL)

---

## 5. Data Flow Diagrams

### 5.1 Context-Level DFD (Level 0)

```
                    Incident Report
  [Employee] ──────────────────────────► [IR SYSTEM]
                                              │
                     ◄───────────────────────┤
                    Status Updates           │
                                             │ Alerts
                    Log Data                 ▼
  [SIEM/IDS] ──────────────────────────► [IR SYSTEM]
                                             │
                    Firewall Rules           │
                    ◄───────────────────────┤
  [Firewall] ◄─────────────────────────────┘
                    Block Attacker C2
```

### 5.2 Level 1 DFD — IR Process

```
Incident Report
     │
     ▼
[1.0 Detect & Classify] ──► Severity Classification ──► [Incident Log]
     │
     ▼
[2.0 Contain]           ──► Isolation Actions     ──► [Action Log]
     │                  ──► Block C2 at Firewall
     ▼
[3.0 Investigate]       ──► Forensic Data         ──► [Evidence Store]
     │                  ──► IOC Extraction
     ▼
[4.0 Eradicate]         ──► Malware Removal       ──► [Clean State]
     │                  ──► Patch Vulnerability
     ▼
[5.0 Recover]           ──► Backup Restore        ──► [Restored Systems]
     │                  ──► Integrity Verification
     ▼
[6.0 Report]            ──► Incident Report       ──► [Stakeholders]
                        ──► Lessons Learned       ──► [IR Plan Update]
```

---

## 6. Sequence Diagram — Phishing Incident Response

```
Employee    Helpdesk     IR Lead    Technical    SIEM
   │           │            │         Analyst       │
   │──Report──►│            │            │           │
   │           │──Create ──►│            │           │
   │           │  Ticket    │            │           │
   │           │            │◄── Alert ──────────────│
   │           │            │   (outbound spike)     │
   │           │            │──Activate IR──►│        │
   │           │            │                │        │
   │           │            │                │──Isolate─►[Host]
   │           │            │                │──Block ──►[Firewall]
   │           │            │                │──Dump ───►[Memory]
   │           │            │                │           │
   │           │            │◄──Log Actions──│           │
   │           │            │                │           │
   │◄──Update──│◄──Notify───│                │           │
```

---

## 7. Activity Diagram — IR Response Flow

```
START
  │
  ▼
[Incident Detected?]
  │ YES
  ▼
[Classify Severity]──► Critical/High ──► [Immediate Response < 1hr]
  │                  ──► Medium/Low  ──► [Scheduled Response]
  ▼
[Notify IR Team]
  │
  ▼
[Isolate Affected Systems] ──► [Preserve Evidence]
  │
  ▼
[Investigate Root Cause]
  │
  ▼
[Eradicate Threat] ──► [Validate Clean State]
  │
  ▼
[Restore from Backup]
  │
  ▼
[Verify Operations Normal?]
  │ NO ──► [Continue Recovery]
  │ YES
  ▼
[Notify Stakeholders]
  │
  ▼
[Conduct Lessons Learned]
  │
  ▼
[Update IR Plan]
  │
  ▼
END
```

---

## 8. State Diagram — Incident Lifecycle

```
                    ┌─────────┐
                    │  NEW    │◄──── Reported by employee or SIEM
                    └────┬────┘
                         │ Validated
                         ▼
                    ┌─────────┐
                    │  OPEN   │◄──── IR team assigned
                    └────┬────┘
                         │ Contained
                         ▼
                    ┌────────────┐
                    │ CONTAINED  │◄──── Systems isolated
                    └────┬───────┘
                         │ Threat removed
                         ▼
                    ┌────────────┐
                    │ ERADICATED │◄──── Malware removed, patched
                    └────┬───────┘
                         │ Systems restored
                         ▼
                    ┌──────────┐
                    │ RESOLVED │◄──── Operations normal
                    └────┬─────┘
                         │ Review complete
                         ▼
                    ┌──────────┐
                    │  CLOSED  │◄──── Lessons learned documented
                    └──────────┘
```

---

## 9. Class Diagram

```
┌──────────────────────────────┐
│         Incident             │
│──────────────────────────────│
│ - incident_id: str           │
│ - date_time: datetime        │
│ - severity: Severity         │
│ - type: IncidentType         │
│ - status: IncidentStatus     │
│──────────────────────────────│
│ + classify_severity()        │
│ + activate_ir_plan()         │
│ + close_incident()           │
└──────────────┬───────────────┘
               │ 1..*
               ▼
┌──────────────────────────────┐
│         Response             │
│──────────────────────────────│
│ - response_id: str           │
│ - incident_id: str           │
│ - phase: IRPhase             │
│ - action: str                │
│ - actor: IRTeamMember        │
│ - timestamp: datetime        │
│──────────────────────────────│
│ + log_action()               │
│ + assign_actor()             │
└──────────────────────────────┘

┌──────────────────────────────┐
│          Asset               │
│──────────────────────────────│
│ - asset_id: str              │
│ - name: str                  │
│ - ip_address: str            │
│ - zone: NetworkZone          │
│ - criticality: Level         │
│──────────────────────────────│
│ + isolate()                  │
│ + restore_from_backup()      │
│ + verify_integrity()         │
└──────────────────────────────┘

<<enum>> IRPhase:
  PREPARATION, DETECTION, CONTAINMENT,
  ERADICATION, RECOVERY, LESSONS_LEARNED

<<enum>> Severity:
  CRITICAL, HIGH, MEDIUM, LOW
```

---

## 10. UI/UX Guidelines

### Design Principles
- **Clarity:** All IR dashboards use plain English — no jargon in user-facing alerts
- **Speed:** Critical alerts displayed in red within 3 seconds of detection
- **Hierarchy:** Most critical information at the top — severity, affected system, time
- **Accessibility:** All text minimum 14pt; color-blind safe palette used

### Color Scheme
| Status | Color | Hex |
|--------|-------|-----|
| Critical | Red | #C0392B |
| High | Orange | #E67E22 |
| Medium | Yellow | #F1C40F |
| Low | Blue | #2E5FA3 |
| Resolved | Green | #1A7A4A |

### Key Screens (Wireframe Descriptions)
1. **Incident Dashboard** — Table of active incidents with severity badges, timestamps, assigned analyst
2. **Incident Detail View** — Timeline of actions, affected assets, evidence log, current phase indicator
3. **Asset Inventory** — List of all assets by zone with health status
4. **Response Playbook** — Step-by-step checklist for current IR phase
5. **Reports View** — Generated incident reports, export to PDF/Word

---

## 11. Technology Stack

| Layer | Technology | Justification |
|-------|-----------|--------------|
| Documentation | Markdown + docx + PDF | GitHub-native, universally readable |
| Version Control | GitHub | Industry standard, required by DEPI |
| Diagram Creation | ASCII / Draw.io / Mermaid | Free, GitHub-renderable |
| Script Automation | Python 3.x | PDF generation, data processing |
| Doc Generation | Node.js + docx library | Professional .docx output |
| SIEM (simulated) | Splunk (reference) | Industry-leading SIEM |
| Network (simulated) | Cisco / pfSense (reference) | Common enterprise stack |

---

## 12. Deployment & Component Diagram

```
┌─────────────────────────────────────────────────────────────────┐
│                        GITHUB REPOSITORY                        │
│  ┌──────────────┐  ┌────────────────┐  ┌─────────────────────┐ │
│  │  Markdown    │  │  .docx / .pdf  │  │  Python/JS Scripts  │ │
│  │  Documents   │  │  Deliverables  │  │  (doc generation)   │ │
│  └──────────────┘  └────────────────┘  └─────────────────────┘ │
└─────────────────────────────────────────────────────────────────┘
                              │
                    ┌─────────▼──────────┐
                    │   GitHub Pages     │  (optional: public site)
                    │  README renders    │
                    │  as project home   │
                    └────────────────────┘

Component Dependencies:
  Python 3.x ──► reportlab ──► PDF files
  Node.js    ──► docx      ──► .docx files
  Markdown   ──► GitHub    ──► rendered documentation
```

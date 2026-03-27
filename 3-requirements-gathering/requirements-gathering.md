# Requirements Gathering
## Cybersecurity Incident Response Framework
**Document Type:** Requirements Gathering | **Section:** 3

---

## Part A — Stakeholder Analysis

### A.1 Stakeholder Identification

| Stakeholder | Type | Interest | Influence |
|-------------|------|----------|-----------|
| IT Security Team | Internal | High | High |
| Executive Management (CISO/CEO) | Internal | High | High |
| End Users / Employees | Internal | Medium | Low |
| Compliance / Legal Team | Internal | High | Medium |
| External Auditors | External | High | Medium |
| Regulatory Bodies (GDPR) | External | High | High |
| Third-party Vendors | External | Medium | Low |
| Academic Assessors (DEPI) | External | High | High |

### A.2 Stakeholder Needs

| Stakeholder | Primary Need | Success Metric |
|-------------|-------------|----------------|
| IT Security Team | Practical, executable IR procedures | All phases actionable in real time |
| Executive Management | Minimal downtime, cost control, regulatory compliance | Breach contained < 4 hours |
| End Users | Clear instructions during an incident | Know who to call and what not to touch |
| Compliance Team | Documentation trail for regulators | GDPR Article 33 notification procedure |
| Academic Assessors | Complete documentation per DEPI guidelines | All 7 sections submitted |

---

## Part B — User Stories & Use Cases

### B.1 User Stories

**As an IT Security Analyst:**
- I want to detect an incident quickly so that I can minimize damage
- I want a severity classification guide so that I know how urgently to respond
- I want evidence collection procedures so that I preserve forensic integrity
- I want containment playbooks so that I know exactly what to do first

**As an Incident Response Lead:**
- I want a clear escalation path so that I can make fast decisions under pressure
- I want pre-defined communication templates so that I can notify stakeholders without delay
- I want a lessons learned template so that every incident improves future response

**As an End User / Employee:**
- I want to know what signs to look for so that I can report suspicious activity
- I want a simple reporting process so that I don't delay the response team
- I want assurance that my data is protected so that I trust the organization

**As a CISO / Executive:**
- I want KPIs and dashboards so that I can measure IR performance
- I want regulatory compliance built into the plan so that I avoid fines
- I want simulation exercises so that the team stays sharp

### B.2 Use Cases

**Use Case 1: Employee Reports Suspicious File**
- Actor: End User
- Trigger: Employee cannot open a file; sees ransomware note
- Steps: Employee calls helpdesk → Helpdesk creates ticket → IR Lead activated → IR Plan initiated
- Outcome: IR Plan activated within 5 minutes of report

**Use Case 2: SIEM Alert — Unusual Outbound Traffic**
- Actor: Security Analyst
- Trigger: SIEM alert fires on outbound traffic volume spike
- Steps: Analyst reviews alert → Correlates with endpoint data → Identifies source IP → Escalates to IR Lead
- Outcome: Source workstation identified and isolated within 15 minutes

**Use Case 3: Ransomware Containment**
- Actor: Technical Lead (Role 2)
- Trigger: Ransomware confirmed on file server
- Steps: Isolate affected host → Preserve memory dump → Disable compromised account → Block C2 at firewall → Document all actions
- Outcome: Spread contained; evidence preserved

**Use Case 4: Post-Incident Lessons Learned**
- Actor: Full IR Team
- Trigger: Incident closed and systems restored
- Steps: Schedule review meeting → Walk through timeline → Identify gaps → Update IR Plan → Assign remediation tasks
- Outcome: Updated IR Plan; remediation tasks assigned

---

## Part C — Functional Requirements

| ID | Requirement | Priority | Owner |
|----|------------|---------|-------|
| FR01 | The IR Plan shall define response procedures for all 6 phases | High | Role 3 |
| FR02 | The system shall classify incidents into 4 severity levels | High | Role 3 |
| FR03 | The architecture shall segment the network into at least 5 zones | High | Role 2 |
| FR04 | The hardening checklist shall cover OS, network, password, patching, and encryption | High | Role 2 |
| FR05 | The IR Plan shall include a severity-based response time matrix | High | Role 3 |
| FR06 | The simulation shall follow a documented attack scenario | High | Role 1 |
| FR07 | The simulation shall produce a timestamped response log | High | Role 2 + Role 3 |
| FR08 | All deliverables shall be uploaded to GitHub | High | All |
| FR09 | The final report shall cover all 7 DEPI documentation sections | High | Role 3 |
| FR10 | The IR Plan shall include access control (RBAC + MFA) procedures | Medium | Role 2 |
| FR11 | The containment phase shall include a decision matrix by incident type | Medium | Role 3 |
| FR12 | The lessons learned section shall produce minimum 5 recommendations | Medium | All |
| FR13 | MITRE ATT&CK techniques shall be mapped for all simulation stages | Medium | Role 1 |
| FR14 | The presentation shall include speaker notes for every slide | Medium | Role 4 |

---

## Part D — Non-Functional Requirements

| ID | Requirement | Category | Metric |
|----|------------|---------|--------|
| NFR01 | All documents shall follow consistent formatting and style | Usability | Peer review pass |
| NFR02 | The IR Plan shall be executable by a team with no prior IR experience | Usability | Simulation executed without external guidance |
| NFR03 | All documents shall load in < 3 seconds from GitHub | Performance | Manual check |
| NFR04 | The GitHub repository shall have at least 5 commits per week | Reliability | GitHub commit log |
| NFR05 | The IR Plan shall comply with NIST SP 800-61 | Security / Compliance | NIST checklist |
| NFR06 | All sensitive scenario data shall be anonymized / simulated | Security | No real credentials or IPs |
| NFR07 | All documents shall be accessible in Markdown and .docx/.pdf | Accessibility | File format check |
| NFR08 | The simulation shall be completable in under 8 hours | Performance | Simulation clock |
| NFR09 | All references shall use proper academic citation format | Quality | Citations present |
| NFR10 | The final report shall not exceed 50 pages | Usability | Page count check |

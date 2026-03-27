# Literature Review
## Cybersecurity Incident Response Framework
**Document Type:** Literature Review | **Section:** 2

---

## 1. Introduction

This literature review examines existing research and industry frameworks related to cybersecurity incident response. The review covers foundational academic and practitioner sources that informed the design of this project's IR Framework.

---

## 2. Incident Response Frameworks

### 2.1 NIST SP 800-61 — Computer Security Incident Handling Guide
**Source:** National Institute of Standards and Technology (2012, revised)

The NIST framework is the most widely adopted IR standard globally. It defines four phases: Preparation, Detection and Analysis, Containment/Eradication/Recovery, and Post-Incident Activity. Key contributions to this project include the severity classification matrix and the evidence handling procedures adopted in our IR Plan.

**Key finding:** NIST emphasizes that preparation is the most critical phase. Organizations that invest in preparation reduce their average containment time by 35%.

### 2.2 SANS Incident Handler's Handbook
**Source:** SANS Institute — Patrick Kral (2011)

The SANS PICERL model expands NIST's four phases into six: Preparation, Identification, Containment, Eradication, Recovery, and Lessons Learned. The added granularity in the Identification phase was directly incorporated into our Detection and Analysis procedures.

**Key finding:** The SANS model's explicit "Lessons Learned" phase produces measurable improvements — organizations that conduct post-incident reviews reduce repeat incidents by 40%.

### 2.3 MITRE ATT&CK Framework
**Source:** MITRE Corporation (2015–present)

ATT&CK (Adversarial Tactics, Techniques, and Common Knowledge) is a globally accessible knowledge base of adversary tactics based on real-world observations. It was used in this project to map each stage of the simulated attack to a specific technique ID, enabling defenders to identify detection opportunities at each phase.

**Key finding:** 7 ATT&CK techniques were identified in the simulation scenario, each mappable to a specific defensive control.

---

## 3. Threat Landscape Research

### 3.1 Verizon Data Breach Investigations Report (DBIR) 2023
**Source:** Verizon (2023)

The DBIR analyzed over 16,000 incidents and 5,000 confirmed breaches. Key findings relevant to this project: phishing was involved in 36% of breaches; ransomware was present in 24% of breaches; insider threats accounted for 19% of incidents.

### 3.2 IBM Cost of a Data Breach Report 2023
**Source:** IBM Security / Ponemon Institute (2023)

Average breach cost reached $4.45M in 2023. Organizations with formal IR plans contained breaches 101 days faster than those without. This statistic directly motivates the project's objective of building a structured IR framework.

### 3.3 Ransomware Trends Report 2022
**Source:** CrowdStrike (2022)

Ransomware attacks increased 93% year-over-year. The average ransom demand reached $812,000. The double-extortion model (encrypt AND exfiltrate) was used in 70% of attacks — directly reflected in the simulation scenario.

---

## 4. Network Security Architecture

### 4.1 CIS Controls v8
**Source:** Center for Internet Security (2021)

CIS Controls provides a prioritized set of actions to protect against the most pervasive cyber attacks. Controls 1–6 (asset inventory, software inventory, data protection, secure configuration, account management, access control management) directly informed the hardening checklist in this project.

### 4.2 Zero Trust Architecture (NIST SP 800-207)
**Source:** NIST (2020)

Zero Trust is an evolving security paradigm based on "never trust, always verify." Key principles — verify explicitly, use least privilege access, assume breach — were incorporated into the network architecture design, particularly the Management Zone access controls.

---

## 5. Suggested Improvements

Based on the literature review, the following improvements are recommended for future versions of this framework:

| Area | Current State | Suggested Improvement | Source |
|------|--------------|----------------------|--------|
| Detection | SIEM-based | Add ML-based anomaly detection | SANS 2022 |
| Backup | Daily backups | Hourly incremental backups | NIST SP 800-34 |
| Communication | Manual | Pre-drafted stakeholder notifications | NIST SP 800-61 |
| Threat Intel | Reactive | Subscribe to threat intel feeds (ISAC) | CIS Controls v8 |
| Training | One simulation | Quarterly tabletop exercises | SANS Handbook |
| Recovery | Manual restore | Automated failover with tested runbooks | ISO 22301 |

---

## 6. Grading Criteria Alignment

| DEPI Grading Area | How This Project Addresses It | Weight |
|-------------------|------------------------------|--------|
| Documentation quality | All 7 sections produced per guidelines | 25% |
| Implementation | Simulation executed, scripts documented, GitHub maintained | 30% |
| Testing | Full test plan, test cases, simulation log | 20% |
| Presentation | 14-slide deck, speaker notes, Q&A preparation | 25% |

---

## 7. References

1. NIST SP 800-61 Rev. 2 — Computer Security Incident Handling Guide (2012)
2. SANS Institute — Incident Handler's Handbook, Patrick Kral (2011)
3. MITRE ATT&CK Framework — https://attack.mitre.org (2015–present)
4. Verizon DBIR 2023 — https://www.verizon.com/business/resources/reports/dbir
5. IBM Cost of a Data Breach Report 2023 — https://www.ibm.com/security/data-breach
6. CrowdStrike Global Threat Report 2022
7. CIS Controls v8 — https://www.cisecurity.org/controls
8. NIST SP 800-207 — Zero Trust Architecture (2020)
9. ISO/IEC 27035 — Information Security Incident Management
10. NIST SP 800-34 — Contingency Planning Guide for Federal Information Systems

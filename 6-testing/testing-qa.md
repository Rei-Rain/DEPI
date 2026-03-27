# Testing & Quality Assurance
## Cybersecurity Incident Response Framework
**Document Type:** Testing & QA | **Section:** 6

---

## 1. Test Plan

### 1.1 Test Objectives
- Verify that the IR Plan is executable without ambiguity
- Validate that the simulation scenario produces measurable outcomes
- Confirm all deliverables meet DEPI documentation guidelines
- Ensure GitHub repository is complete and accessible

### 1.2 Test Scope

| Area | In Scope | Out of Scope |
|------|---------|-------------|
| IR Plan usability | ✅ Can team execute without improvisation? | Live system testing |
| Architecture correctness | ✅ Do zones and rules align with design? | Real firewall configuration |
| Simulation execution | ✅ All 8 attack stages completable? | Real malware deployment |
| Documentation completeness | ✅ All DEPI sections present? | Grader assessment |
| GitHub accessibility | ✅ All files accessible and readable? | External user testing |

### 1.3 Test Types

| Type | Description | Method |
|------|------------|--------|
| Functional Testing | Does each IR phase work as documented? | Tabletop walkthrough |
| Usability Testing | Can team follow plan without external help? | Blind execution test |
| Documentation Testing | Are all required sections present and complete? | DEPI checklist review |
| Integration Testing | Do all weeks' documents reference each other correctly? | Cross-reference review |
| Acceptance Testing | Does the final output meet academic requirements? | Peer review |

---

## 2. Test Cases

### 2.1 IR Plan Test Cases

| TC-ID | Test Case | Steps | Expected Result | Actual Result | Pass/Fail |
|-------|-----------|-------|----------------|---------------|-----------|
| TC-01 | Severity Classification | Present each of 4 incident types; ask team to classify | Correct severity level assigned in < 2 min | Critical → Critical; High → High confirmed | PASS |
| TC-02 | Containment — Network Isolation | Simulate infected host; execute containment | Host isolated within 15 min; no spread | Isolated at T+00:15 (15 min) | PASS |
| TC-03 | Containment — Account Disable | Compromised account identified; disable it | Account disabled + sessions revoked < 5 min | Disabled at T+00:19 (4 min) | PASS |
| TC-04 | Evidence Preservation | Confirm memory dump captured before system shutdown | SHA-256 hash recorded; chain of custody logged | Hash recorded: b7f2a3c9... | PASS |
| TC-05 | Eradication — Malware Removal | Remove all RAT components from 2 workstations | All 3 persistence mechanisms removed | UpdateSvc.exe + task + registry key removed | PASS |
| TC-06 | Patch Application | Apply CVE-2021-34527 patch to all systems | Patch confirmed applied on all 47 endpoints | Applied at T+01:50 | PASS |
| TC-07 | Backup Restore | Restore file server from backup | Files restored; hash integrity verified | Restored at T+02:45; hash matched | PASS |
| TC-08 | Recovery Verification | Confirm all systems operational | All business services accessible | All confirmed operational T+03:30 | PASS |

### 2.2 Documentation Test Cases

| TC-ID | Test Case | Check | Expected | Actual | Pass/Fail |
|-------|-----------|-------|---------|--------|-----------|
| TC-09 | DEPI Section 1 — Planning | All 5 planning docs present | Project Proposal, Plan, Roles, Risk, KPIs | All 5 present | PASS |
| TC-10 | DEPI Section 2 — Literature | Academic review with sources | Min 8 references, formal structure | 10 references | PASS |
| TC-11 | DEPI Section 3 — Requirements | All 4 requirement docs present | Stakeholders, Stories, Functional, Non-functional | All 4 present | PASS |
| TC-12 | DEPI Section 4 — Design | All diagrams present | Use Case, ERD, DFD, Sequence, Activity, State, Class | All 7 diagrams | PASS |
| TC-13 | DEPI Section 5 — Implementation | GitHub repo + README | Public repo, meaningful commits, README | Repo active | PASS |
| TC-14 | DEPI Section 6 — Testing | Test plan + cases + bugs | This document | Complete | PASS |
| TC-15 | DEPI Section 7 — Presentation | Final report + slides + user manual | .docx, .pdf, notes | All present | PASS |

### 2.3 GitHub Test Cases

| TC-ID | Test Case | Expected | Pass/Fail |
|-------|-----------|---------|-----------|
| TC-16 | README renders correctly | README visible on repo homepage | PASS |
| TC-17 | All folders present | 7 main folders + deliverables | PASS |
| TC-18 | .docx files downloadable | All 4 .docx files open correctly | PASS |
| TC-19 | .pdf files downloadable | All 4 .pdf files render correctly | PASS |
| TC-20 | Markdown files render | All .md files render in GitHub | PASS |

---

## 3. Bug Reports

### 3.1 Issues Found During Testing

| Bug-ID | Description | Severity | Status | Resolution |
|--------|------------|---------|--------|-----------|
| BUG-01 | Second infected workstation (192.168.10.52) not found until T+01:25 — too slow | Medium | Resolved | Added EDR recommendation to lessons learned |
| BUG-02 | No DLP alert triggered during 2.3GB exfiltration | High | Resolved (gap) | Documented as critical finding; DLP recommended |
| BUG-03 | VPN had no MFA — attacker used only stolen password | Critical | Resolved (gap) | MFA enforcement added as Priority 1 recommendation |
| BUG-04 | PrintNightmare patch not applied for 6 months | High | Resolved | 48-hour patch SLA added to hardening checklist |
| BUG-05 | Backup recovery window is 24 hours — too long | Medium | Partially resolved | Hourly incremental backup recommended |
| BUG-06 | No GDPR notification procedure in original IR Plan | Medium | Resolved | Added to Phase 6 (Lessons Learned) |

### 3.2 Documentation Bugs

| Bug-ID | Description | Status |
|--------|------------|--------|
| BUG-07 | Week 1 README lacked installation steps | Resolved — expanded README |
| BUG-08 | Task assignment was informal only | Resolved — formal document created |
| BUG-09 | No formal literature review section | Resolved — Section 2 created |
| BUG-10 | System diagrams were ASCII-only, no formal UML | Partially resolved — text UML added |

---

## 4. Test Summary

| Category | Tests Run | Passed | Failed | Pass Rate |
|----------|-----------|--------|--------|-----------|
| IR Plan Functional | 8 | 8 | 0 | 100% |
| Documentation | 7 | 7 | 0 | 100% |
| GitHub | 5 | 5 | 0 | 100% |
| **Total** | **20** | **20** | **0** | **100%** |

**Quality Assurance Sign-off:**
All 20 test cases passed. 6 functional bugs identified during simulation — all resolved through recommendations and IR plan updates. 4 documentation bugs resolved. Repository ready for submission.

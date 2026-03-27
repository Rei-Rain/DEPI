# KPIs — Key Performance Indicators
## Cybersecurity Incident Response Framework
**Document Type:** KPIs | **Section:** 1 — Project Planning & Management

---

## 1. Project Success KPIs

| KPI | Target | Measurement Method |
|-----|--------|--------------------|
| All DEPI deliverables submitted | 100% | Checklist against guidelines |
| GitHub commits per week | Min 5 commits/week | GitHub commit history |
| Documentation quality | All sections complete, no gaps | Peer review checklist |
| Presentation coverage | All 7 sections of DEPI guidelines addressed | Slide count + content map |

---

## 2. Incident Response Framework KPIs

### 2.1 Detection KPIs
| KPI | Target | Actual (Simulation) | Status |
|-----|--------|---------------------|--------|
| Mean Time to Detect (MTTD) | < 15 minutes | 8 minutes | ✅ MET |
| Alert accuracy (no false positives) | > 90% | 100% | ✅ MET |
| Detection source identified | Yes | Yes — SIEM outbound alert | ✅ MET |

### 2.2 Response KPIs
| KPI | Target | Actual (Simulation) | Status |
|-----|--------|---------------------|--------|
| Mean Time to Contain (MTTC) | < 60 minutes | 32 minutes | ✅ MET |
| Mean Time to Eradicate | < 4 hours | 1 hr 45 min | ✅ MET |
| Mean Time to Recovery (MTTR) | < 8 hours | 3 hrs 30 min | ✅ MET |
| Ransom paid | $0 | $0 | ✅ MET |

### 2.3 System Availability KPIs
| KPI | Target | Result |
|-----|--------|--------|
| Critical systems restored | 100% | 100% (3/3 systems) |
| Data recovery rate from backup | > 95% | ~99% (12 files lost) |
| Management Zone uptime during incident | 100% | 100% |
| Systems protected by segmentation | > 80% | 94% (47/50) |

### 2.4 Security Posture KPIs
| KPI | Target | Result |
|-----|--------|--------|
| Hardening controls implemented | > 40 controls | 42 controls documented |
| Network zones segmented | 5 zones | 5 zones implemented |
| IR Plan phases covered | 6 phases | 6 phases (NIST + SANS) |
| MITRE ATT&CK techniques mapped | All attack stages | 7/7 stages mapped |

### 2.5 Team Performance KPIs
| KPI | Target | Result |
|-----|--------|--------|
| IR Plan adherence during simulation | 100% | 100% — no improvisation |
| All team members present on simulation day | 4/4 | 4/4 |
| Post-incident review conducted | Within 2 weeks | Documented same day |
| Recommendations produced | Minimum 5 | 6 recommendations |

---

## 3. KPI Dashboard Summary

| Category | KPIs Met | KPIs Total | % |
|----------|---------|------------|---|
| Detection | 3 | 3 | 100% |
| Response | 4 | 4 | 100% |
| Availability | 4 | 4 | 100% |
| Security Posture | 4 | 4 | 100% |
| Team Performance | 5 | 5 | 100% |
| **Overall** | **20** | **20** | **100%** |

---

## 4. KPI Improvement Targets (Post-Project)

| KPI | Current | Improved Target | Action Required |
|-----|---------|----------------|----------------|
| MTTD | 8 min | < 5 min | Deploy EDR on all endpoints |
| Data loss window | 24 hrs | < 1 hr | Move to hourly incremental backups |
| Exfiltration detection | Not detected | Detect within 10 min | Deploy DLP solution |
| MFA coverage | 60% of access points | 100% | Enforce MFA on VPN |

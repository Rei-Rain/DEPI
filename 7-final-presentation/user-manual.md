# User Manual
## Cybersecurity Incident Response Framework
**Document Type:** User Manual | **Section:** 7 — Final Presentation & Reports
**Audience:** End users, IT staff, non-technical stakeholders

---

## 1. Introduction

This manual explains how to use the Cybersecurity Incident Response Framework. It covers what to do when you suspect an incident, how to report it, and what to expect from the IR team.

---

## 2. Who Is This For?

| Reader | What to Read |
|--------|-------------|
| All employees | Sections 3 and 4 — how to recognize and report incidents |
| IT helpdesk | Sections 3, 4, and 5 — receiving and escalating reports |
| IR team members | Sections 5 and 6 — executing the IR plan |
| Management | Sections 7 and 8 — understanding outcomes and reporting |

---

## 3. How to Recognize a Cybersecurity Incident

**Stop and report immediately if you see any of these:**

| Sign | What It Could Mean |
|------|--------------------|
| Files have unusual extensions (.locked, .encrypted) | Ransomware attack |
| You cannot open files you could open before | Ransomware or malware |
| Your computer is running very slowly | Malware or cryptominer |
| You received an email asking for your password | Phishing attempt |
| You clicked a link and were asked to log in | Credential harvesting |
| Your account password suddenly doesn't work | Account takeover |
| You see programs you didn't install | Malware or RAT |
| A ransom note appears on your screen | Active ransomware |
| Colleagues report the same file access issues | Network-wide ransomware |

---

## 4. How to Report an Incident

### Step 1 — Do NOT:
- ❌ Turn off your computer (this destroys forensic evidence)
- ❌ Click on anything suspicious again
- ❌ Try to fix it yourself
- ❌ Tell the attacker you know they're in the system
- ❌ Pay any ransom without authorization

### Step 2 — DO:
- ✅ Disconnect from Wi-Fi or unplug your ethernet cable if told to by IT
- ✅ Call the IT helpdesk immediately: **[Helpdesk Number]**
- ✅ Send an email to: **security@organization.com**
- ✅ Note the time you first noticed the issue
- ✅ Do not discuss the incident on regular communication channels (use phone)

### Step 3 — Information to have ready:
- What you saw / what happened
- When did you first notice it?
- What were you doing just before it happened?
- Did you click any links or open any files?
- Which computer / which account?

---

## 5. What Happens After You Report

```
You Report ──► IT Helpdesk creates ticket ──► IR Lead activated
                                                     │
                                              Severity assessed
                                                     │
                                   ┌─────────────────┴──────────────────┐
                                   │                                    │
                              CRITICAL/HIGH                         LOW/MEDIUM
                         Immediate response                    Scheduled response
                         within 1–4 hours                      within 24–72 hours
```

**You will be contacted by the IR team if:**
- Your workstation needs to be taken offline temporarily
- Your account credentials need to be reset
- You need to provide additional information about what happened

**You do NOT need to do anything else** — the IR team handles the investigation.

---

## 6. IR Team Quick Reference Card

### Phase 1 — When Incident is Reported
- [ ] Create incident ticket
- [ ] Classify severity (Critical / High / Medium / Low)
- [ ] Alert IR team lead
- [ ] Start timer

### Phase 2 — Containment (do this FIRST)
- [ ] Isolate affected host from network (do NOT power off)
- [ ] Disable compromised user account
- [ ] Block attacker C2 at firewall
- [ ] Capture memory dump
- [ ] Document every action with timestamp

### Phase 3 — Investigation
- [ ] Analyze memory dump
- [ ] Check SIEM logs for timeline
- [ ] Identify all affected systems
- [ ] Collect IOCs

### Phase 4 — Eradication (Eradicate threat)
- [ ] Remove all malware and backdoors
- [ ] Patch the exploited vulnerability
- [ ] Reset all compromised credentials
- [ ] Scan all adjacent systems

### Phase 5 — Recovery
- [ ] Verify backup integrity
- [ ] Restore from clean backup
- [ ] Reconnect systems under enhanced monitoring
- [ ] Confirm operations normal

### Phase 6 — After the Incident
- [ ] Notify stakeholders
- [ ] Conduct lessons learned meeting (within 2 weeks)
- [ ] Update IR Plan
- [ ] Submit all documentation to GitHub

---

## 7. Severity Reference Card

| If you see... | Severity | Response starts in |
|--------------|---------|-------------------|
| Ransomware / data breach / full system down | CRITICAL | < 1 hour |
| Unauthorized access / active malware spreading | HIGH | < 4 hours |
| Single infected workstation / policy violation | MEDIUM | < 24 hours |
| Suspicious activity / minor issue | LOW | < 72 hours |

---

## 8. Contacts

| Role | Contact Method |
|------|---------------|
| IT Helpdesk | Phone: [number] / Email: helpdesk@org.com |
| IR Lead | Phone: [number] (24/7 for Critical incidents) |
| CISO | Phone: [number] (Critical incidents only) |
| Legal / Compliance | Email: legal@org.com (data breach notification) |

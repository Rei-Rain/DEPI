# Presentation Notes — Final Presentation
**Cybersecurity Incident Response Framework**
> Author: Role 4 (Presenter Lead) | All members review before delivery

---

## Presentation Structure

| Slide | Title | Speaker | Time |
|-------|-------|---------|------|
| 1 | Title Slide | Role 4 | 1 min |
| 2 | Project Objective | Role 4 | 1 min |
| 3 | Team Roles | Role 4 | 1 min |
| 4 | Week 1 — Threat Landscape | Role 1 | 3 min |
| 5 | Week 1 — Network Discovery | Role 2 | 3 min |
| 6 | Week 2 — IR Plan Overview | Role 3 | 3 min |
| 7 | Week 2 — Secure Architecture | Role 2 | 3 min |
| 8 | Week 3 — Attack Scenario | Role 1 | 2 min |
| 9 | Week 3 — Response Timeline | Role 2 | 3 min |
| 10 | Week 3 — Results | Role 3 | 2 min |
| 11 | Key Findings and Gaps | Role 4 | 3 min |
| 12 | Recommendations | Role 4 | 2 min |
| 13 | Conclusion | Role 4 | 2 min |
| 14 | Q&A | All | 5 min |
| **Total** | | | **~34 min** |

---

## Slide-by-Slide Speaker Notes

---

### Slide 1 — Title Slide

**Visual:** Project title, team name, date, university/institution name

**Speaker (Role 4):**
> "Good [morning/afternoon]. We're here today to present our four-week cybersecurity project: Building a Comprehensive Incident Response Framework. My name is [name], and I'm presenting alongside [names]. Over the next 30 minutes, we'll walk you through everything we built — from research and planning, to a live simulation of a ransomware attack and our team's response."

**Transition:** "Let's start with why this project matters."

---

### Slide 2 — Project Objective

**Visual:** Single clear objective statement. Three bullet points: Plan → Execute → Review

**Speaker (Role 4):**
> "The objective of this project was to build a complete, end-to-end incident response framework from scratch. Not just a document — a working system that we actually tested.
>
> We structured this across four weeks: Week 1 — we researched the threat landscape. Week 2 — we built the plan and the architecture. Week 3 — we simulated a real attack and executed our plan. Week 4 — we compiled everything into this final report and presentation.
>
> Every deliverable in this project was designed to be something a real organization could actually use."

**Transition:** "Here's how we divided the work across the four of us."

---

### Slide 3 — Team Roles

**Visual:** 4 cards — one per person, color-coded, name + role + one-line description

**Speaker (Role 4):**
> "We assigned roles based on the skills needed for each function. [Role 1] led all our research and threat intelligence work. [Role 2] owned everything technical — the architecture, the tools, and running the simulation. [Role 3] wrote and compiled all our formal documents. And I managed the slides and presentation delivery.
>
> Importantly — everyone contributed to every week. The roles determined who led each piece, not who worked in isolation."

**Transition:** "Let's start with what we learned in Week 1."

---

### Slide 4 — Week 1: Threat Landscape

**Visual:** Table — 6 threat types with brief description and one key stat each

**Speaker (Role 1):**
> "Week 1 was about understanding the enemy before we tried to defend against them.
>
> We researched six major threat categories. The most important finding for our project was that over 80% of all cybersecurity incidents begin with phishing. Not sophisticated zero-day exploits — a fake email. That shaped everything we built in Week 2.
>
> We also studied the CIA Triad — Confidentiality, Integrity, Availability — which became the framework for how we evaluated every security decision. If a control doesn't protect at least one of these three, it shouldn't be in the plan."

**Transition:** "Role 2 will now cover what we found about how attackers map a network before they attack."

---

### Slide 5 — Week 1: Network Discovery

**Visual:** Simple diagram — attacker outside network, arrows showing ping sweep → port scan → enumeration

**Speaker (Role 2):**
> "One of the most important things a defender needs to understand is what an attacker sees when they look at your network.
>
> We documented the full reconnaissance toolkit — ping sweeps to find live hosts, port scanning to find open services, service version detection to find known CVEs, and enumeration to extract usernames and file shares.
>
> Here's the key takeaway: every single one of these techniques maps to a specific defensive control. Ping sweep is stopped by blocking ICMP. Port scanning reveals open ports — so you close the ones you don't need. Version detection finds outdated software — so you patch. Understanding the attack is the first step to blocking it."

**Transition:** "With that foundation, we moved into planning. Role 3 will walk you through the IR Plan."

---

### Slide 6 — Week 2: IR Plan Overview

**Visual:** Flowchart — 6 phases in sequence with brief label for each

**Speaker (Role 3):**
> "In Week 2, we produced a formal Incident Response Plan based on two industry standards — NIST SP 800-61 and the SANS PICERL model. We combined both into a six-phase plan.
>
> Phase 1 is Preparation — everything you set up before an incident happens. Phase 2 is Detection and Analysis — identifying that something is wrong. Phase 3 is Containment — stopping the spread. Phase 4 is Eradication — removing the threat. Phase 5 is Recovery — restoring systems. Phase 6 is Lessons Learned — improving for next time.
>
> The plan also includes a severity matrix — Critical incidents get a response within one hour, High within four hours, and so on. Having that pre-defined means the team doesn't waste time deciding how serious something is — the plan tells them."

**Transition:** "Role 2 will cover the secure architecture we designed to support that plan."

---

### Slide 7 — Week 2: Secure Architecture

**Visual:** Network diagram — 5 zones stacked with labels and arrows showing traffic flow

**Speaker (Role 2):**
> "We designed a five-zone network architecture following the Defense in Depth principle.
>
> The outer layer is the DMZ — where public-facing web and DNS servers live. Behind that is a second firewall with a WAF and IDS. Inside the network, we separated employee workstations, servers, and the management zone into different VLANs that cannot directly communicate with each other.
>
> The critical design decision was this: the database server is only reachable from the application server. Not from employee workstations. Not from the DMZ. Just the app server. This alone prevents a huge class of attacks.
>
> We also produced a 40-item hardening checklist — covering OS hardening, network hardening, password policy, patch management timelines, and encryption standards."

**Transition:** "With the plan built and the architecture designed, Week 3 was time to test it."

---

### Slide 8 — Week 3: Attack Scenario

**Visual:** Timeline bar — 8 attack stages across 6 hours, color-coded

**Speaker (Role 1):**
> "For Week 3, I designed the attack scenario that Role 2 would simulate. We called it Operation Locked Vault.
>
> The attack follows a realistic chain: a Finance employee receives a spear-phishing email impersonating HR. They click a link, enter their Microsoft 365 credentials on a fake page, and those credentials are immediately stolen by the attacker.
>
> From there, the attacker uses those credentials to VPN into the company network. They install a Remote Access Trojan, escalate privileges using a real unpatched vulnerability called PrintNightmare, move laterally to the file server using a technique called Pass-the-Hash, exfiltrate 2.3 gigabytes of financial records, and then deploy LockBit ransomware.
>
> All of this happened in just over six hours. The victim organization had no idea until an employee tried to open a file."

**Transition:** "Role 2 will now walk you through exactly how our IR team responded."

---

### Slide 9 — Week 3: Response Timeline

**Visual:** Table — 4 response phases with time taken, target, and pass/fail

**Speaker (Role 2):**
> "When the incident was discovered, we activated the Week 2 IR Plan immediately.
>
> Detection took 8 minutes from when the ransomware deployed — we had SIEM alerts on unusual outbound traffic volume that pointed us to the right workstation quickly.
>
> Containment took 32 minutes. We isolated two systems from the network, disabled the compromised user account, blocked the attacker's C2 server at the firewall, and captured memory dumps for forensic analysis — all before powering anything off.
>
> Eradication took another hour and 45 minutes. We found the RAT on two workstations, removed all persistence mechanisms, reset all potentially exposed credentials, and patched the PrintNightmare vulnerability that was the root cause of the privilege escalation.
>
> Recovery was completed 45 minutes after that. We restored the file server from a clean verified backup, rebuilt both workstations from baseline images, and brought everything back online under enhanced monitoring."

**Transition:** "Role 3 will summarize the results."

---

### Slide 10 — Week 3: Results

**Visual:** 4 key numbers highlighted large — 8 min / 32 min / 3.5 hrs / $0

**Speaker (Role 3):**
> "Four numbers summarize what happened:
>
> 8 minutes to detect. 32 minutes to contain. 3 and a half hours to full recovery. And zero dollars in ransom paid.
>
> We met every response time target in our IR Plan. All three affected systems were restored. The network segmentation we designed in Week 2 limited the damage — only two workstations and the file server were compromised. The database, application server, and all 45 other endpoints were untouched.
>
> The only irreversible loss was approximately 12 files created on the day of the attack that weren't captured in the overnight backup."

**Transition:** "But the simulation also revealed some serious gaps. Role 4 will cover those."

---

### Slide 11 — Key Findings and Gaps

**Visual:** 6-row table — gap, priority (color-coded), one-line fix

**Speaker (Role 4):**
> "The simulation was valuable not just because it proved our plan works — but because it showed us exactly where we're still vulnerable.
>
> The most critical finding: there was no Multi-Factor Authentication on the VPN. That single missing control is what allowed the attacker to access the entire internal network using just a stolen password. One SMS code would have stopped the attack at Stage 2.
>
> The second major finding: the PrintNightmare vulnerability had been publicly disclosed and patched by Microsoft six months before our simulation. It was never applied. A strict patch management policy would have removed the attacker's privilege escalation path entirely.
>
> We also found that 2.3 gigabytes of sensitive financial data left the network completely undetected — because there was no Data Loss Prevention solution in place. By the time we noticed the exfiltration, it had already completed."

**Transition:** "Here's what we recommend to fix these gaps."

---

### Slide 12 — Recommendations

**Visual:** 6 recommendations numbered, icons, priority labels

**Speaker (Role 4):**
> "We have six recommendations, in priority order.
>
> One — enforce MFA on VPN immediately. This is the single highest-impact fix with the lowest implementation cost.
>
> Two — enforce a 48-hour patch window for Critical severity vulnerabilities. PrintNightmare was patched. It just wasn't applied. The process needs teeth.
>
> Three — deploy a Data Loss Prevention solution within 30 days. You cannot respond to data theft you cannot see.
>
> Four — deploy advanced email filtering. Phishing is the entry point for over 80% of incidents. Blocking it at the mail gateway stops attacks before they reach employees.
>
> Five — roll out Endpoint Detection and Response to all endpoints. We found a second infected workstation 85 minutes into the response because we had no visibility.
>
> Six — move from daily to hourly incremental backups. This reduces the maximum data loss window from 24 hours to 1 hour."

**Transition:** "Let me close with our final takeaway."

---

### Slide 13 — Conclusion

**Visual:** Three pillars — People, Process, Technology — with one key point under each

**Speaker (Role 4):**
> "The most important lesson from this entire project is simple: technical controls alone are not enough.
>
> The attack succeeded initially not because our firewall failed or our architecture was wrong. It succeeded because a person clicked a link, and a process — MFA enforcement — was missing. The technology was fine.
>
> Effective cybersecurity requires all three pillars working together. People need training and awareness. Processes need to be enforced, not just documented. Technology needs to be deployed, configured, and kept current.
>
> This project gave us a working framework that addresses all three. The IR Plan is the process. The hardening checklist addresses the technology. And the simulation — and the gaps it revealed — is directly about people and process.
>
> Thank you. We're happy to take questions."

---

### Slide 14 — Q&A

**Speaker:** All members

**Likely questions and suggested answers:**

**Q: Why did you choose a ransomware scenario specifically?**
> "Ransomware was the fastest-growing threat category at the time of our research — up 93% year-on-year. It also tests the full IR lifecycle: detection, containment, eradication, and recovery all matter. Simpler attacks don't stress-test the full plan."

**Q: Would you pay the ransom in a real scenario?**
> "Our recommendation is no. Paying the ransom funds criminal operations, provides no guarantee of decryption, and in some jurisdictions creates legal liability. Having a tested backup and recovery process is the correct alternative — which is why backup integrity is a critical part of our plan."

**Q: How realistic is a 32-minute containment time?**
> "It's achievable with preparation. The key was having the IR Plan already written and practiced. The team didn't spend time deciding what to do — we executed pre-planned steps. Organizations without a plan typically take hours just to understand the situation."

**Q: What's the most important thing an organization can do right now?**
> "Enforce Multi-Factor Authentication on everything. It's the single highest-impact control available, it costs almost nothing to implement, and it would have stopped this specific attack at Stage 2."

# Week 1 Research Report — Foundation and Awareness
**Cybersecurity Incident Response Framework Project**
> Status: Complete | Author: Role 3 (compiled) | Input: Role 1 + Role 2

---

## Table of Contents
1. Introduction
2. Core Cybersecurity Concepts
3. Common Threat Types
4. Network Discovery Techniques
5. Key Findings Summary
6. References

---

## 1. Introduction

Cybersecurity is the practice of protecting systems, networks, and data from digital attacks, unauthorized access, and damage. As organizations increasingly depend on digital infrastructure, understanding the threat landscape and fundamental security principles becomes critical.

This report covers the foundational concepts that underpin the cybersecurity incident response framework developed in this project. It documents core security principles, common attack vectors, and the technical methods attackers use to discover and map networks.

---

## 2. Core Cybersecurity Concepts

### 2.1 The CIA Triad

The CIA Triad is the foundational model of information security:

| Principle | Definition | Example Threat |
|-----------|-----------|----------------|
| Confidentiality | Data accessible only to authorized users | Data breach, eavesdropping |
| Integrity | Data is accurate and untampered | Man-in-the-middle, data corruption |
| Availability | Systems accessible when needed | DDoS attack, ransomware |

### 2.2 Defense in Depth

A layered security strategy where multiple controls protect assets. Layers include physical security, network security, host security, application security, and data security.

### 2.3 Principle of Least Privilege

Every user and process should have only the minimum permissions needed. This limits damage if an account is compromised.

### 2.4 Zero Trust Security Model

"Never trust, always verify." No user or device is trusted by default — every access request must be authenticated and authorized.

---

## 3. Common Threat Types

### 3.1 Malware

| Type | Description |
|------|-------------|
| Virus | Attaches to files and spreads |
| Trojan | Disguised as legitimate software |
| Ransomware | Encrypts files, demands payment |
| Spyware | Silently collects user data |
| Worm | Self-replicates across networks |
| Rootkit | Hides attacker presence in OS |

### 3.2 Phishing

Social engineering that tricks users into revealing credentials or installing malware. Phishing is responsible for over 80% of reported security incidents.

Types: Email phishing, spear phishing, whaling, smishing, vishing.

### 3.3 DDoS Attack

Floods a target with traffic from multiple sources to exhaust resources and deny service to legitimate users.

### 3.4 Ransomware Attack Chain

1. Initial access (phishing or exposed RDP)
2. Establish persistence
3. Lateral movement across network
4. Data exfiltration
5. File encryption
6. Ransom demand

### 3.5 Insider Threats

Threats from employees or contractors: malicious insiders (intentional), negligent insiders (accidental), and compromised insiders (account takeover).

### 3.6 Man-in-the-Middle (MitM)

Attacker intercepts communications between two parties. Methods include ARP poisoning and SSL stripping.

---

## 4. Network Discovery Techniques

Attackers use these techniques in the reconnaissance phase to map targets before launching attacks.

| Technique | Tool | Purpose |
|-----------|------|---------|
| Ping Sweep | nmap -sn | Find live hosts |
| Port Scan | nmap -sS | Find open ports |
| Service Detection | nmap -sV | Find software versions |
| OS Fingerprinting | nmap -O | Identify operating systems |
| Enumeration | enum4linux, snmpwalk | Extract users and shares |

For full technical detail see network-discovery.md

---

## 5. Key Findings Summary

| Finding | Implication |
|---------|-------------|
| CIA Triad guides all security decisions | IR phases must address all three principles |
| Phishing is the top initial access vector | Detection must include email monitoring |
| Ransomware follows a predictable chain | Early detection at lateral movement prevents full encryption |
| Network scanning reveals attack surface | All unnecessary ports must be closed in Week 2 |
| Insider threats bypass perimeter controls | Internal user monitoring is essential |

---

## 6. References

1. NIST SP 800-61 Rev. 2 — Computer Security Incident Handling Guide
2. SANS Institute — Incident Handler's Handbook
3. MITRE ATT&CK Framework — https://attack.mitre.org
4. CVE Database — https://cve.mitre.org
5. Nmap Official Documentation — https://nmap.org/docs.html
6. Verizon Data Breach Investigations Report (DBIR) 2023

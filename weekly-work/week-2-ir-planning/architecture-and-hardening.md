# Secure Network Architecture & System Hardening Report
**Cybersecurity Incident Response Framework — Week 2**
> Status: Complete | Author: Role 2 (Technical Lead)

---

## Table of Contents
1. Secure Network Architecture
2. Architecture Component Descriptions
3. System Hardening Checklist
4. Access Control Implementation
5. Security Monitoring Points

---

## 1. Secure Network Architecture

The architecture below follows a **Defense in Depth** model with segmented zones. Each zone has strict access controls limiting lateral movement.

```
                        INTERNET
                           │
                    ┌──────▼──────┐
                    │   FIREWALL  │  (Perimeter — blocks all
                    │  (Layer 1)  │   inbound except allowed)
                    └──────┬──────┘
                           │
              ┌────────────▼────────────┐
              │        DMZ ZONE         │
              │  ┌─────────┐ ┌───────┐  │
              │  │  Web    │ │  DNS  │  │
              │  │ Server  │ │Server │  │
              │  └─────────┘ └───────┘  │
              └────────────┬────────────┘
                           │
                    ┌──────▼──────┐
                    │  INTERNAL   │  (WAF + IDS/IPS)
                    │  FIREWALL   │
                    │  (Layer 2)  │
                    └──────┬──────┘
                           │
         ┌─────────────────┼──────────────────┐
         │                 │                  │
  ┌──────▼──────┐  ┌───────▼──────┐  ┌───────▼──────┐
  │  USER LAN   │  │ SERVER ZONE  │  │  MGMT ZONE   │
  │             │  │              │  │              │
  │ Workstations│  │ App Server   │  │ SIEM / IDS   │
  │ (VLAN 10)  │  │ DB Server    │  │ Admin Tools  │
  │             │  │ File Server  │  │ (VLAN 99)   │
  └─────────────┘  └──────────────┘  └──────────────┘
         │                 │
         └────── VPN ──────┘
              (Remote Access)
```

### Network Zones Summary

| Zone | VLAN | Purpose | Trust Level |
|------|------|---------|-------------|
| DMZ | VLAN 20 | Public-facing services (web, DNS) | Untrusted |
| User LAN | VLAN 10 | Employee workstations | Low trust |
| Server Zone | VLAN 30 | Internal application and data servers | Medium trust |
| Management | VLAN 99 | Security tools, admin access | High trust |
| VPN | VLAN 50 | Remote access tunnel | Verified only |

---

## 2. Architecture Component Descriptions

### 2.1 Perimeter Firewall (Layer 1)
- Blocks all inbound traffic by default
- Allows only ports 80 (HTTP), 443 (HTTPS), and 53 (DNS) inbound to DMZ
- All outbound traffic logged
- Stateful packet inspection enabled

### 2.2 DMZ (Demilitarized Zone)
- Hosts only public-facing services
- No direct communication allowed from DMZ to internal network
- Web server and DNS server are the only systems in this zone
- Regular vulnerability scanning of all DMZ systems

### 2.3 Internal Firewall (Layer 2)
- Web Application Firewall (WAF) inspects HTTP/HTTPS traffic
- IDS/IPS monitors all traffic between DMZ and internal network
- Blocks all direct DMZ-to-Server Zone traffic
- Only specific application ports permitted between zones

### 2.4 User LAN (VLAN 10)
- Employee workstations
- No direct access to Server Zone — must go through application tier
- Internet access allowed through proxy with content filtering
- No peer-to-peer communication between workstations

### 2.5 Server Zone (VLAN 30)
- Application server, database server, file server
- Database accessible only from application server (not directly from User LAN)
- All server-to-server traffic logged
- Regular patching schedule enforced

### 2.6 Management Zone (VLAN 99)
- Highest security zone
- SIEM, IDS, and admin tools reside here
- Access restricted to named administrator accounts only
- Requires MFA + VPN for all access
- All sessions recorded

---

## 3. System Hardening Checklist

### 3.1 Operating System Hardening

#### Windows Systems
- [ ] Enable automatic Windows Update and set to install critical patches within 48 hours
- [ ] Disable unused services (Telnet, FTP, Remote Registry)
- [ ] Enable Windows Defender Firewall on all hosts
- [ ] Disable SMBv1 (known ransomware propagation vector — EternalBlue)
- [ ] Enable BitLocker disk encryption on all workstations
- [ ] Configure account lockout: lock after 5 failed attempts for 30 minutes
- [ ] Disable AutoRun / AutoPlay on all media
- [ ] Enable audit logging: logon events, account management, privilege use, object access
- [ ] Remove all default/guest accounts
- [ ] Rename default Administrator account

#### Linux Systems
- [ ] Apply all security updates — run `apt update && apt upgrade` or equivalent
- [ ] Disable root SSH login — set `PermitRootLogin no` in `/etc/ssh/sshd_config`
- [ ] Change default SSH port from 22
- [ ] Enable UFW or iptables firewall
- [ ] Remove unused packages and services
- [ ] Set file permissions: sensitive files should be 600 or 640 max
- [ ] Enable auditd for system call logging
- [ ] Configure fail2ban to block brute force attacks
- [ ] Disable USB storage devices where not needed
- [ ] Use sudo instead of direct root access

### 3.2 Network Hardening

- [ ] Change all default router/switch/AP credentials immediately
- [ ] Disable Telnet — use SSH only for device management
- [ ] Enable SSH v2 only (disable SSHv1)
- [ ] Implement VLAN segmentation as per architecture
- [ ] Enable port security on switches (limit MAC addresses per port)
- [ ] Disable unused switch ports and put them in a dead VLAN
- [ ] Enable DHCP snooping to prevent rogue DHCP servers
- [ ] Enable Dynamic ARP Inspection (DAI) to prevent ARP spoofing
- [ ] Disable CDP/LLDP on external-facing interfaces
- [ ] Configure syslog to send all logs to central SIEM

### 3.3 Password Policy

| Policy Item | Requirement |
|-------------|-------------|
| Minimum length | 12 characters |
| Complexity | Upper + lower + number + special character |
| Maximum age | 90 days |
| Password history | Last 12 passwords cannot be reused |
| Account lockout | 5 failed attempts → 30-minute lockout |
| MFA | Required for all admin and remote access |
| Default passwords | Must be changed immediately on all new systems |

### 3.4 Patch Management

| Priority | Patch Type | Maximum Patch Window |
|----------|-----------|---------------------|
| Critical (CVSS 9-10) | RCE, privilege escalation | 48 hours |
| High (CVSS 7-8.9) | Authentication bypass, data exposure | 7 days |
| Medium (CVSS 4-6.9) | Local exploits, DoS | 30 days |
| Low (CVSS < 4) | Minor vulnerabilities | 90 days |

### 3.5 Encryption Standards

- [ ] All data in transit encrypted with TLS 1.2 or higher (disable TLS 1.0 and 1.1)
- [ ] Disable SSL 2.0 and SSL 3.0 completely
- [ ] All data at rest encrypted using AES-256
- [ ] VPN uses IKEv2 with AES-256 and SHA-256
- [ ] Certificates use RSA 2048-bit or ECDSA 256-bit minimum
- [ ] HSTS (HTTP Strict Transport Security) enabled on all web servers
- [ ] Disable weak cipher suites (RC4, DES, 3DES)

### 3.6 Application Security

- [ ] Remove all default application credentials
- [ ] Disable directory listing on web servers
- [ ] Remove server version banners from HTTP headers
- [ ] Implement Content Security Policy (CSP) headers
- [ ] Enable X-Frame-Options to prevent clickjacking
- [ ] Input validation on all user inputs
- [ ] Parameterized queries to prevent SQL injection
- [ ] Regular DAST/SAST scans on all web applications

---

## 4. Access Control Implementation

### 4.1 RBAC Implementation

```
Administrator
    └── Full system + network access
        └── Requires MFA + recorded session

Security Analyst
    └── Read-only access to logs, SIEM, IDS alerts
        └── Cannot modify system configurations

Developer
    └── Development environment only
        └── No access to production systems

End User
    └── Email + business applications + file shares
        └── No admin rights on local machine

Service Accounts
    └── Specific application only
        └── No interactive login allowed
```

### 4.2 MFA Requirements

| System | MFA Method | Enforcement |
|--------|-----------|-------------|
| VPN | TOTP (Google Authenticator) | Mandatory |
| Admin Console | Hardware token (YubiKey) | Mandatory |
| Email (Remote) | Push notification | Mandatory |
| Cloud Services | TOTP or push | Mandatory |
| Local workstation | Password only | Optional |

---

## 5. Security Monitoring Points

These are the key points in the architecture where monitoring must be active:

| Location | What to Monitor | Alert On |
|----------|----------------|---------|
| Perimeter Firewall | All denied inbound traffic | Port scans, repeated denials |
| DMZ | Web server access logs | SQL injection attempts, 4xx/5xx spikes |
| Internal Firewall | Zone-crossing traffic | Any DMZ-to-Server direct connection |
| User LAN | Outbound traffic volume | Large data uploads, unusual destinations |
| Server Zone | File access and DB queries | Bulk data access, off-hours activity |
| Management Zone | Admin login attempts | Failed logins, off-hours access |
| All Systems | Authentication logs | Brute force, credential stuffing |

---

## References
1. CIS Benchmarks — https://www.cisecurity.org/cis-benchmarks
2. NIST SP 800-123 — Guide to General Server Security
3. NSA Cybersecurity Technical Reports — https://www.nsa.gov/cybersecurity
4. Microsoft Security Baselines
5. DISA STIGs — https://public.cyber.mil/stigs

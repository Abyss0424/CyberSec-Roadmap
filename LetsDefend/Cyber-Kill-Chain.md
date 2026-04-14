# Cyber Kill Chain

**Platform:** LetsDefend  
**Module:** SOC Analyst Learning Path — Cyber Kill Chain  
**Author:** Julio  
**Status:** ✅ Completed

---

## What is the Cyber Kill Chain?

A framework created by Lockheed Martin in 2011 to model the stages of a cyber attack. It helps SOC analysts understand attack progression, identify where in the chain a threat was detected, and determine where security controls failed or succeeded.

The chain has **7 sequential steps** — if an attacker fails at any stage, the attack cannot proceed to the next.

---

## The 7 Phases

### 1. Reconnaissance

The attacker collects information about the target to identify attack vectors and expand the attack surface.

| Type | Description |
|------|-------------|
| **Passive** | Gathering info without directly interacting with the target (e.g., web archives, OSINT) |
| **Active** | Directly engaging with the target to extract information (e.g., querying a web server for version details) |

**Attacker actions:**
- Obtaining server/software version information
- Gathering OSINT about the organization
- Collecting employee email addresses
- Harvesting personal info via social media
- Detecting internet-facing devices (Shodan, Zoomeye)
- Identifying security vulnerabilities on exposed servers
- Mapping the organization's IP address blocks
- Identifying third-party vendors

**Defender actions:**
- External pentests to discover information disclosure
- Threat Intelligence to find leaked organizational data
- Removing publicly available internal documents
- Firewall and traffic monitoring on internet-facing assets
- Patching promptly to reduce exposed vulnerabilities

---

### 2. Weaponization

The attacker uses reconnaissance data to build or acquire the tools needed for the attack. The victim is unaware at this stage.

**Attacker actions:**
- Pairing an exploit with a backdoor payload
- Obfuscating malware to evade AV/EDR detection
- Crafting social engineering hooks (phishing emails, malicious links)

**Defender actions:**
- Vulnerability management — finding CVEs before the attacker does
- Threat Intelligence — updating firewall/IDS rules with new malware signatures
- Hardening — disabling unnecessary services, ports, and protocols

---

### 3. Delivery

The first direct interaction with the victim. The attacker transmits the weapon to the target environment.

**Attacker delivery methods:**
- **Email:** Phishing with malicious attachments or URLs
- **Web:** Hosting malware for the victim to download
- **Social Media:** Distributing malicious links or files
- **Direct Access:** Uploading malware via an exploited vulnerability
- **Physical:** USB drops to bypass network perimeter defenses

**Defender actions:**
- Email Security Gateways, Firewalls, and Antivirus to filter content
- Sandboxing suspicious files and URLs
- Logging and traffic anomaly monitoring
- Security awareness training for employees

> 💡 **Key insight:** This is the best phase to break the kill chain — strong perimeter defenses and user education can stop the attack here before any system is compromised.

---

### 4. Exploitation

The weapon is activated. The attacker triggers a vulnerability or executes malicious code on the victim's system — the first actual operation on the target.

**Attacker actions:**
- Triggering hardware or software vulnerabilities
- Executing the delivered malware
- Leveraging pre-collected system knowledge for compatibility

**Defender actions:**
- EDR for real-time endpoint monitoring
- Regular vulnerability scanning and CVE patching
- Principle of Least Privilege enforcement
- Developer security training (secure coding)
- Regular penetration testing

---

### 5. Installation

The attacker establishes **persistence** — ensuring continued access even after reboots or patching.

**Attacker actions:**
- Deploying droppers to install more complex malware
- Privilege escalation to gain Admin/SYSTEM rights
- Installing Web Shells on servers
- Creating Scheduled Tasks or Services for automatic malware execution
- Modifying Firewall rules to allow outbound connections

**Defender actions:**
- **"Assume Breach"** mindset — act as if the attacker is already inside
- Threat Hunting for anomalies in network and endpoints
- Integrity monitoring on critical files and system paths
- EDR/XDR for unauthorized configuration changes and suspicious process trees
- Application control — only allowing digitally signed executables
- Just-In-Time privilege management

---

### 6. Command & Control (C2)

The attacker establishes a communication channel between the compromised machine and their external server, enabling remote command execution.

**Attacker actions:**
- Configuring a C2 server to receive connections from the victim
- Instructing malware to "phone home" to attacker infrastructure
- Using beacons (periodic signals) to maintain the connection

> ⚠️ Attackers commonly hide C2 traffic inside legitimate protocols (HTTPS, DNS) to blend in with normal traffic.

**Defender actions:**
- Cyber Threat Intelligence (CTI) — blocking known malicious IPs and domains
- Network Security Monitoring — detecting beacon patterns (e.g., a host connecting to an unknown external IP every 30 seconds)
- Scanning endpoints for known C2 frameworks (Cobalt Strike, Sliver, Metasploit)
- Egress filtering — restricting outbound traffic from internal servers

---

### 7. Actions on Objectives

The attacker executes their primary mission. Every previous phase was preparation for this moment.

**Attacker actions (depends on motivation):**
- **Data Exfiltration** — stealing sensitive documents or credentials
- **Ransomware** — encrypting files and demanding payment
- **Sabotage** — deleting or manipulating critical data
- **Lateral Movement** — using the compromised host as a pivot to attack other internal systems
- **Credential Harvesting** — scraping memory or files for passwords

**Defender actions:**
- DLP (Data Loss Prevention) — detecting and blocking unauthorized data transfers
- Network anomaly detection — monitoring for traffic spikes or unusual internal scanning
- Principle of Least Privilege on databases and critical folders
- EDR for detecting ransomware encryption or credential dumping
- Egress filtering to limit which hosts can communicate externally

---

## Practical Exercise — APT38 / Lazarus Group (2019)

**Target:** Financial sector institution  
**Attack chain mapping:**

| # | Action | Kill Chain Phase |
|---|--------|-----------------|
| 1 | APT38 targeted a financial institution | Reconnaissance |
| 2 | Conducted reconnaissance on the organization's website for several days | Reconnaissance |
| 3 | Identified CVE-2019-0604 in Microsoft SharePoint | Reconnaissance |
| 4 | CVE-2019-0604 was exploited | Exploitation |
| 5 | PowerShell Empire backdoor deployed | Installation |

**Key insight:** Identifying a specific vulnerability (CVE-2019-0604) is part of **Reconnaissance**, not Exploitation — because the attacker is still in the information-gathering phase, not yet executing the attack.

**Reconnaissance actions count: 3**

---

## Practical Exercise — Defense Sector USB Drop Attack

**Attack chain mapping:**

| # | Action | Kill Chain Phase |
|---|--------|-----------------|
| 1 | IP addresses detected via Shodan and Zoomeye | Reconnaissance |
| 2 | Windows OS identified via OSINT | Reconnaissance |
| 3 | Malware embedded in putty.exe using Metasploit | Weaponization |
| 4 | Malware transferred to USB sticks | Weaponization |
| 5 | USB sticks left near the institution | Delivery |
| 6 | Employee plugged USB into corporate computer | Delivery |
| 7 | Employee executed putty.exe | Exploitation |
| 8 | Attacker gained remote command execution via reverse connection | Exploitation |
| 9 | Attacker added a Scheduled Task for persistence | Installation |
| 10 | EDR flagged the Scheduled Task as suspicious | — (Detection) |
| 11 | SOC analyst investigated and contained the attack | — (Response) |

**Weaponization actions: 2 | Delivery actions: 2**

---

*Part of my cybersecurity training portfolio — SOC → Cloud Security Blue Team path*

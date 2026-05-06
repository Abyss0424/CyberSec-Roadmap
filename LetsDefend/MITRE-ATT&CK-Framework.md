# MITRE ATT&CK Framework

**Platform:** LetsDefend  
**Module:** SOC Analyst Learning Path — MITRE ATT&CK Framework  
**Author:** Julio  
**Status:** ✅ Completed

---

## What is MITRE ATT&CK?

A globally accessible knowledge base of adversary behavior based on real-world observations.  
**ATT&CK** stands for **Adversarial Tactics, Techniques, and Common Knowledge**.

Think of it as a periodic table for cyberattacks — a standardized language for describing how attackers operate across different platforms (Windows, Linux, Cloud, ICS, Mobile).

- **Introduced:** 2013 by MITRE Corporation
- **Continuously updated** to reflect the evolving threat landscape
- Considered an **essential, foundational resource** for the entire cybersecurity industry

---

## Core Structure

| Component | The Question It Answers | Example |
|-----------|------------------------|---------|
| **Tactic** | *Why* — the adversary's objective | Persistence |
| **Technique** | *How* — the specific method used | Scheduled Task |
| **Sub-Technique** | *How exactly* — a more granular breakdown | Scheduled Task via Windows Task Scheduler |
| **Procedure** | *How in the real world* — tool/malware used by a specific group | APT39 using Mimikatz for credential dumping |

---

## Why It Matters for SOC Analysts

- **Reference & Roadmap:** Anticipate what an attacker might do next based on known patterns
- **Detection & Mitigation:** Build more effective detection rules and response playbooks
- **Alert Mapping:** Link specific alerts to known threat actor behaviors
- **Reporting:** Standardized language for incident reports and forensic documentation
- **Proactive Defense:** Identify gaps in current defenses before a real breach occurs

---

## The Three Primary Matrices

| Matrix | Focus | Notes |
|--------|-------|-------|
| **Enterprise** | Traditional corporate systems (Windows, Linux, Cloud, Network) | Largest and most detailed |
| **Mobile** | Android and iOS devices | Significantly less data than Enterprise |
| **ICS** | Industrial Control Systems (factories, power grids) | Specialized hardware and physical processes |

### Enterprise Sub-Matrices (7)
- **PRE** — Pre-compromise preparation steps
- **Windows, macOS, Linux** — Operating system coverage
- **Cloud, Network, Containers** — Modern infrastructure coverage

### Mobile Sub-Matrices
- Android
- iOS

---

## The 14 Enterprise Tactics

Tactics represent the adversary's **objective** at each stage. Attackers may skip steps or loop back.

| # | Tactic | Goal |
|---|--------|------|
| 1 | **Reconnaissance** | Gather information about the target |
| 2 | **Resource Development** | Build infrastructure (accounts, domains, tools) |
| 3 | **Initial Access** | Get into the network |
| 4 | **Execution** | Run malicious code |
| 5 | **Persistence** | Maintain a foothold after reboots or patching |
| 6 | **Privilege Escalation** | Gain Admin or Root-level permissions |
| 7 | **Defense Evasion** | Avoid detection by security tools |
| 8 | **Credential Access** | Steal usernames and passwords |
| 9 | **Discovery** | Map out the internal environment |
| 10 | **Lateral Movement** | Move from one system to another |
| 11 | **Collection** | Gather data for the final objective |
| 12 | **Command & Control (C2)** | Communicate with compromised systems |
| 13 | **Exfiltration** | Steal the collected data |
| 14 | **Impact** | Manipulate, interrupt, or destroy data/systems |

> **Mobile** also has 14 tactics, adding *Network Effects* and *Remote Service Effects*.  
> **ICS** has 12 tactics, adding *Inhibit Response Function* and *Impair Process Control*.

---

## Techniques & Sub-Techniques

| Matrix | Techniques | Sub-Techniques |
|--------|------------|----------------|
| Enterprise | 193 | 401 |
| Mobile | 66 | 41 |
| ICS | 79 | 0 |

- A **gray bar** next to a technique name in the ATT&CK Matrix indicates it contains sub-techniques
- **Procedures** identify the specific real-world tools or malware used — the "fingerprints" of a threat group

---

## Mitigations

Mitigations are the defensive measures used to **prevent** a technique from succeeding.  
Every mitigation has a unique **ID**, a **Name**, and a **Description** of how to implement it.

| Matrix | Total Mitigations |
|--------|------------------|
| Enterprise | 43 |
| Mobile | 11 |
| ICS | 51 (largest set) |

**Mapping example:**

| Mitigation | ID | Addresses |
|------------|----|-----------|
| Filter Network Traffic | M1037 | Adversary-in-the-Middle (T1557), ARP Cache Poisoning, LLMNR/NBT-NS Poisoning |
| Antivirus/Antimalware | M1049 | Multiple malware-based techniques |
| Account Use Policies | M1036 | Credential-based attacks |

---

## APT Groups

Advanced Persistent Threat (APT) groups are organized threat actors — sometimes state-sponsored — that conduct targeted, systematic attacks.

Every group entry in the framework includes:
- **ID** — Unique identifier (e.g., G0032 for Lazarus Group)
- **Name** — Primary name and aliases
- **Description** — History, known campaigns, and associated group names

### Group Motivations

| Motivation | Description |
|------------|-------------|
| **Financial** | Conducting attacks primarily to generate money |
| **National/Political** | State-sponsored groups pursuing government objectives |
| **Specific Mission** | Targeted operations for a precise, defined assignment |

**Mapping example — Lazarus Group (G0032):**

| Component | Detail |
|-----------|--------|
| Techniques used | Access Token Manipulation (T1134.002), Account Discovery (T1087.002) |
| Software leveraged | AppleJeus (S0584), AuditCred (S0347) |

---

## Software

The framework catalogs programs and tools used by APT groups during attacks.

Every software entry includes:
- **ID** — Unique alphanumeric identifier (e.g., S0066)
- **Name** — Tool or malware name
- **Description** — Functionality, programming language, and operational history

### Software Categories

| Category | Description | Examples |
|----------|-------------|---------|
| **Malware** | Programs built for malicious purposes (RATs, backdoors, ransomware) | 3PARA RAT (S0066), 4H RAT (S0065) |
| **Tools** | Commercial, open-source, or built-in utilities abused by attackers | Mimikatz, PsExec, Cobalt Strike |

> At the time of this training, the framework cataloged **718 software entries** — constantly growing.

**Correlation example:**

| Software | Technique Used | Group |
|----------|---------------|-------|
| 3PARA RAT (S0066) | Uses HTTP for C2 communication | Putter Panda |

---

## Key Takeaway

The MITRE ATT&CK Framework connects four layers into a complete picture of any attack:

```
GROUP (Who) → TECHNIQUE (How) → SOFTWARE (With what) → MITIGATION (How to stop it)
```

As a SOC analyst, mapping an alert to an ATT&CK technique transforms a raw log entry into an actionable intelligence report.

---

*Part of my cybersecurity training portfolio — SOC → Cloud Security Blue Team path*

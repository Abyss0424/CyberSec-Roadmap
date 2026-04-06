# SOC Fundamentals

**Platform:** LetsDefend  
**Module:** SOC Fundamentals  
**Author:** Julio  
**Status:** ✅ Completed

---

## Module Objective

Understand what a SOC is, how it is structured, the roles within the team, and the basic workflow of a security analyst.

---

## Key Concepts

### What is a SOC?

A SOC (Security Operations Center) is an Information Security team whose purpose is to detect, analyze, and respond to cybersecurity incidents.

---

### Roles Within a SOC

| Role | Responsibility |
|------|----------------|
| **SOC Analyst L1** | Alert triage — first line of response |
| **SOC Analyst L2** | Investigate the root cause of the incident |
| **SOC Analyst L3** | Propose remediation strategies and solutions |
| **Incident Responder** | Initial detection and assessment of breaches to contain active attacks |
| **Threat Hunter** | Proactive profile that searches for hidden threats (such as APTs) that automated tools fail to detect |
| **Security Engineer** | Builds and maintains the SOC's technical infrastructure (SIEM, SOAR) |
| **SOC Manager** | Operational and strategic management: budgets, staffing, and general coordination |

---

### Alert Types

| Type | Description |
|------|-------------|
| **True Positive** | Real alert — malicious activity was detected and is actually occurring |
| **False Positive** | False alarm — the system flagged a legitimate activity as a threat |
| **False Negative** | Worst-case scenario — a real threat passed through without triggering any alert |
| **True Negative** | No alert generated because there is genuinely no threat present |

---

### Basic Triage Workflow

First response to an alert, executed primarily by the L1 analyst.

```
Step 1 — Collection
  └── Receive the alert from the SIEM or monitoring tools

Step 2 — Validation
  └── Is this a True Positive (real threat) or a False Positive (false alarm)?

Step 3 — Classification & Prioritization
  └── Assign severity level: Low / Medium / High / Critical

Step 4 — Initial Analysis (Contextualization)
  └── Identify which users, devices, or data are involved

Step 5 — Escalation or Closure
  └── Complex threat → escalate to L2/L3
  └── False alarm or minor event → close the ticket
```

---

## SOC Tools

| Tool | Function |
|------|----------|
| **SIEM** | Central platform that collects, stores, and correlates logs from across the network to generate alerts |
| **EDR** | Installed on endpoints (laptops, servers) — monitors suspicious behavior and responds to threats in real time |
| **SOAR** | Connects different security tools to automate repetitive tasks and accelerate incident response |
| **Threat Intelligence Feed** | External data stream about global threats (malicious IPs, new malware, attacker tactics) that guides the SOC on what to look for |

---

*Part of my cybersecurity training portfolio — SOC → Cloud Security Blue Team path*

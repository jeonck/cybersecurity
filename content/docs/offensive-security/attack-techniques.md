---
weight: 10010
title: "Systematic Classification of Attack Techniques"
description: "A security analysis framework that classifies cyberattacks by stage, layer, and objective to optimize defense strategy and threat intelligence use."
icon: "swords"
date: "2026-08-18"
lastmod: "2026-08-18"
draft: false
---

## I. Overview

```mermaid
%%{init: { 'theme': 'base', 'themeVariables': { 'edgeLabelBackground': '#fff' }}}%%
flowchart LR
    A["Scattered, Fragmented\nThreats"] -- "Framework-based classification\n(Cyber Kill Chain)" --> B["Systematic, Structured\nDefense"]
    style A fill:#f9f9f9,stroke:#333,stroke-width:3px
    style B fill:#e1f5fe,stroke:#01579b,stroke-width:3px
```

**Definition**: A security analysis framework that systematizes cyberattacks by stage, layer, and objective in order to optimize defense strategy development and the use of threat intelligence.

**Features**:  
( **Threat Visibility** ) Classifies an attacker's tactics, techniques, and procedures ( **TTPs** ) using a standardized language, enabling the creation of sophisticated detection rules.  
( **Proactive Defense** ) Enables a staged blocking strategy based on the Cyber Kill Chain, which cuts the chain of an attack at any link.  
( **Collaboration Optimization** ) Maximizes the efficiency of security operations ( **SecOps** ) by sharing threat information and standardizing the incident response process.

## II. Mechanism & Components

### A. Attack Flow by Kill Chain Stage

```mermaid
flowchart LR
    A["① Reconnaissance\nGathering target information"] -->|"OSINT / scanning"| B["② Weaponization\nCrafting the malware"]
    B -->|"Packaging the exploit"| C["③ Delivery\nEmail / USB"]
    C -->|"Phishing / drive-by"| D["④ Exploitation\nTriggering the vulnerability"]
    D -->|"Code execution"| E["⑤ Installation\nInstalling a RAT / backdoor"]
    E -->|"Establishing persistence"| F["⑥ Command & Control (C2)\nRemote control channel"]
    F -->|"Issuing commands"| G["⑦ Actions on Objectives\nData theft / destruction"]
```

> **Key Point**: Blocking the early stages of the kill chain (reconnaissance and delivery) is the most cost-effective defense strategy.

### B. Attack Techniques and Response Strategy by Kill Chain Stage

| Kill Chain Stage | Key Attack Techniques | Detection / Response |
|------------|-------------|----------------|
| Reconnaissance | OSINT, Shodan scanning, DNS enumeration | Minimize externally exposed information, operate honeypots |
| Weaponization | Exploit kits, macro malware creation | Collect IoCs based on threat intelligence |
| Delivery | Spear-phishing email, drive-by download | Email sandboxing, URL filtering |
| Exploitation | Zero-day, SQL injection, buffer overflow | Patch management, WAF, IPS |
| Installation | Rootkits, web shells, registry persistence | EDR, integrity monitoring |
| Command & Control (C2) | HTTP/DNS tunneling, Tor-based covert channels | Anomalous traffic detection, DNS sinkholing |
| Actions on Objectives | Ransomware, data exfiltration, destruction | UEBA, DLP, backup and recovery |

## III. Advanced Topics & Comparison

### A. Classification by OSI Layer and Attack Target

| Attack Layer | Representative Techniques | Objective | Key Countermeasures |
|---------|------------|------|-------------|
| Application layer | SQL injection, XSS, CSRF, XXE | Data theft / privilege theft | WAF, secure coding, SAST/DAST |
| Network layer | DDoS, IP spoofing, MITM, ARP spoofing | Service disruption / eavesdropping | IDS/IPS, anti-DDoS, VPN |
| System layer | Ransomware, buffer overflow, privilege escalation | System takeover / file encryption | EDR, least privilege, ASLR |
| Social engineering layer | Phishing, smishing, voice phishing, pretexting | Credential theft / trust abuse | Security awareness training, enforced MFA |

### B. Latest Advanced Attack Trends

```mermaid
flowchart TD
    T["Advanced Attack Trends"] --> APT["APT\n(Advanced Persistent Threat)"]
    T --> SC["Supply Chain\nAttack"]
    T --> FL["Fileless\nAttack"]

    APT --> APT1["Long-term concealment,\nthen theft of core assets\nResponse: threat hunting / UEBA"]
    SC --> SC1["Compromise via SW update\nor build systems, large-scale damage\nResponse: SBOM / code signing"]
    FL --> FL1["Abuses memory and legitimate\ntools (LOLBin), leaves no file trace\nResponse: memory forensics / EDR"]
```

| Attack Type | Characteristics | Representative Cases | Key Response |
|---------|------|---------|---------|
| APT (Advanced Persistent Threat) | Long-term dwell time, focused targeting, multi-stage attack | Lazarus, APT41 | Threat hunting, MITRE ATT&CK mapping |
| Supply Chain Attack | Indirect infiltration through trusted software or vendors | SolarWinds, XZ Utils | SBOM management, code signing verification |
| Fileless Attack | Abuses legitimate processes (PowerShell, WMI) | Cobalt Strike | Behavior-based detection, memory analysis |

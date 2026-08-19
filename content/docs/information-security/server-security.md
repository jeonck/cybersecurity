---
weight: 1240
title: "Systematic Server Defense Strategy"
description: "A layered defense strategy that hardens servers and applies secure-OS access control to protect confidentiality, integrity, and availability."
icon: "dns"
date: "2026-08-18"
lastmod: "2026-08-18"
draft: false
---

## I. Overview

```mermaid
%%{init: { 'theme': 'base', 'themeVariables': { 'edgeLabelBackground': '#fff' }}}%%
flowchart LR
    A["Vulnerable server\n(default configuration)"] -- "Hardening / secure OS" --> B["Hardened\nserver (hardened host)"]
    style A fill:#f9f9f9,stroke:#333,stroke-width:3px
    style B fill:#e1f5fe,stroke:#01579b,stroke-width:3px
```

**Definition**: Security activities that remove vulnerabilities in server components — the operating system, applications, database, and more — and block unauthorized access, thereby securing the confidentiality, integrity, and availability of the service.

**Key Defense Strategies**:  
( **Host Fortification** ) **Hardening**: Minimizing the attack surface by removing unnecessary services and accounts and applying the latest security patches  
( **Kernel-Level Hardening** ) **Secure OS**: Implementing strong access control through a reference monitor and **MAC (Mandatory Access Control)**  
( **Layered Defense** ) **Defense in Depth**: Layering security controls across the physical, network, system, application, and data tiers  

## II. Mechanism & Components

```mermaid
flowchart LR
    subgraph L1["① Physical Security"]
        P1["Access control\nmonitoring\nCCTV"]
    end
    subgraph L2["② Network Security"]
        P2["Firewall (FW)\nIPS / IDS\nport blocking"]
    end
    subgraph L3["③ System (OS) Security"]
        P3["Hardening\naccess control\npatch management"]
    end
    subgraph L4["④ Application Security"]
        P4["WAF\nsecure coding\nSAST / DAST"]
    end
    subgraph L5["⑤ Data Security"]
        P5["Encryption\n(at-rest / in-transit)\naccess-log management"]
    end

    L1 --> L2 --> L3 --> L4 --> L5
```

| Category | Key Security Technologies & Activities | Description |
|-----|------------------|---------|
| Physical Security | Access control, monitoring | Restricting physical access to data centers and server rooms |
| Network Security | Firewall (FW), IPS/IDS | Blocking unnecessary ports, network-based intrusion detection and prevention |
| System (OS) Security | Hardening, access control | Removing unnecessary services/accounts, patching kernel and OS vulnerabilities |
| Application Security | WAF, secure coding | Defending against web vulnerabilities (SQLi, XSS) and secure source-code development |
| Data Security | Encryption, access-log management | Encrypting data at rest and data in transit |

## III. Comparison & Application

| Model | Key Features | Mechanism |
|------|---------|---------|
| Mandatory Access Control (MAC) | Access is granted based on security levels set by an administrator | Security kernel, rule-based |
| Discretionary Access Control (DAC) | The resource owner grants permissions | ID-based, permission granting |
| Role-Based Access Control (RBAC) | Permissions are assigned based on the user's job/role | Role-centered within the organization |

```mermaid
flowchart LR
    USER["User\naccess request"] --> REF["Reference monitor\nmediates all access"]
    REF --> MAC["MAC\ncompares security levels\n(label-based)"]
    REF --> DAC["DAC\nchecks owner permissions\n(ACL-based)"]
    REF --> RBAC["RBAC\nchecks role permissions\n(role-based)"]
    MAC -->|"Level satisfied"| ALLOW["Access allowed"]
    DAC -->|"Permission granted"| ALLOW
    RBAC -->|"Role matches"| ALLOW
    MAC -->|"Level not satisfied"| DENY["Access denied + audit log"]
```

Most enterprise systems need RBAC as the default and MAC only where regulation demands it, not the other way around — DAC alone is too permissive for anything beyond personal workstations, while pure MAC's rigid labeling overhead rarely justifies itself outside government or defense-grade classification requirements. RBAC hits the maintainability sweet spot for the access-review workload most organizations actually have to sustain.

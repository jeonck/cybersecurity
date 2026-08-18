---
weight: 1220
title: "CIA Triad"
description: "The three core elements of information security — confidentiality, integrity, and availability — and how they trade off against each other."
icon: "security"
date: "2026-08-18"
lastmod: "2026-08-18"
draft: false
---

## I. Overview

```mermaid
%%{init: { 'theme': 'base', 'themeVariables': { 'edgeLabelBackground': '#fff' }}}%%
flowchart LR
    A["Information asset\n(raw data)"] -- "Security controls (applying CIA)" --> B["Secure\nstate"]
    style A fill:#f9f9f9,stroke:#333,stroke-width:3px
    style B fill:#e1f5fe,stroke:#01579b,stroke-width:3px
```

**Definition**: The state achieved by putting physical, technical, and administrative measures in place to preserve the confidentiality, integrity, and availability of information assets.

**Core Security Elements**:  
( **Confidentiality** ) Preventing eavesdropping and leakage so that only authorized users can access information  
( **Integrity** ) The state in which information is guaranteed to be accurate and complete, unaltered by unauthorized parties  
( **Availability** ) The state in which authorized users can access information and services whenever they need them  

## II. Mechanism & Components

### A. Detailed Comparison of Confidentiality, Integrity, and Availability

| Category | Confidentiality | Integrity | Availability |
|------|------------------------|------------------|----------------------|
| Definition | Only authorized users can access information | Information is not illegally altered | Information and services can be used whenever needed |
| Core Goal | Preserving secrecy | Guaranteeing accuracy and completeness | Ensuring service continuity |
| Security Threats | Eavesdropping, social engineering, sniffing | Message tampering, replay attacks | DoS/DDoS, ransomware, physical destruction |
| Countermeasures | Encryption, access control, DRM | Hash functions, digital signatures, MAC | Backups, redundancy (DR/BCP), load balancing |

## III. Advanced Topics & Comparison

### A. Security Trade-offs

```mermaid
flowchart LR
    C2["Strengthening confidentiality\ncomplex encryption"] -->|"Reduced speed"| A2["Reduced availability\nuser inconvenience"]
    I2["Strengthening integrity\ndeep traffic inspection"] -->|"Service delay"| A3["Reduced availability\nslower response time"]
```

### B. Optimization Strategies (Security Balance)

- **Risk-based design**: Apply differentiated security levels depending on asset value — prioritizing confidentiality (financial data) or availability (process control systems)
- **Defense in depth**: Design a layered security architecture so that if one element is compromised, the others can compensate

---
weight: 3060
title: "CASB (Cloud Access Security Broker)"
description: "A security control point placed between on-premises infrastructure and cloud services that unifies policy enforcement and visibility across SaaS usage."
icon: "cloud_sync"
date: "2026-08-18"
lastmod: "2026-08-18"
draft: false
---

## I. Overview

```mermaid
%%{init: { 'theme': 'base', 'themeVariables': { 'edgeLabelBackground': '#fff' }}}%%
flowchart LR
    A["Shadow IT\nproliferation"] -- "Unified cloud\nsecurity policy" --> B["Visibility and\nthreat defense"]
    style A fill:#f9f9f9,stroke:#333,stroke-width:3px
    style B fill:#e1f5fe,stroke:#01579b,stroke-width:3px
```

**Definition**: A CASB is a security solution or service placed between an organization's on-premises infrastructure and its cloud services that applies security policy consistently and provides visibility across that boundary.

**Features**:  
( **Shadow IT Control** ) Identifies and manages the risk of unauthorized cloud services used outside organizational control.  
( **Data Leakage Prevention** ) Blocks the exfiltration of sensitive information through DLP capabilities optimized for cloud environments.  
( **Account Protection** ) Detects abnormal logins and applies access control to counter cloud account takeover attacks.

## II. Mechanism & Components

### A. The Four Core Security Pillars of CASB

- **Visibility**: Identifies every cloud service in use across the organization and assesses its risk (Shadow IT detection)
- **Data Security**: Applies DLP (data loss prevention), encryption, and access control to data stored in the cloud
- **Compliance**: Continuously checks compliance with regulations such as data protection laws and PCI-DSS
- **Threat Protection**: Detects abnormal logins (anomaly detection), blocks malware propagation, and performs user and entity behavior analytics (UEBA)

### B. Comparison of CASB Deployment Methods

| Category | **API Mode** (Out-of-Band) | **Proxy Mode** (In-Line) |
|------|---------------------------|--------------------------|
| **Operating Principle** | Calls the cloud service's API directly | Sits in the traffic path for real-time monitoring |
| **Performance Impact** | No added network latency | Traffic passes through the broker, which can affect performance |
| **Coverage** | Focused on managed cloud services | Can also control Shadow IT and unmanaged apps |
| **Timing** | Analysis occurs after data has already been stored | Enables real-time blocking at the point of data transfer |
| **Characteristics** | Easy to install but can be bypassed | Configured as a forward or reverse proxy |

## III. Advanced Topics & Comparison

### CASB vs. Traditional Security Solutions (DLP, Proxy)

| Comparison Item | Traditional DLP / Proxy Solutions | CASB (Cloud Native) |
|----------|-----------------------|---------------------|
| **Security Scope** | Internal network and endpoints | External cloud services such as SaaS and PaaS |
| **Identification Unit** | Centered on IP addresses and URLs | User accounts and app-level actions (e.g. share, delete) |
| **Access Control** | Simple allow / deny | Fine-grained, behavior-based control (context-aware) |
| **Visibility Scope** | Limited to internal network traffic | Includes external traffic from mobile and remote work |

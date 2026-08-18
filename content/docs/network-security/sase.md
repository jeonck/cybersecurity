---
weight: 2100
title: "SASE (Secure Access Service Edge)"
description: "A cloud-native architecture that converges networking functions such as SD-WAN with security services such as ZTNA and CASB on a single platform."
icon: "cloud_sync"
date: "2026-08-18"
lastmod: "2026-08-18"
draft: false
---

## I. Overview

```mermaid
%%{init: { 'theme': 'base', 'themeVariables': { 'edgeLabelBackground': '#fff' }}}%%
flowchart LR
    A["Network + security\n(managed separately)"] -- "Cloud-native convergence" --> B["SASE\n(single platform)"]
    style A fill:#f9f9f9,stroke:#333,stroke-width:3px
    style B fill:#e1f5fe,stroke:#01579b,stroke-width:3px
```

**Definition**: A cloud-native architecture that delivers networking functions such as **SD-WAN** together with security services such as next-generation firewall, **CASB**, and **ZTNA** from a single cloud platform.

**Features**:  
( **Perimeter Collapse** ) The spread of cloud adoption and remote work has exposed the limits of the traditional perimeter-based security model.  
( **Network Bottlenecks** ) Backhauling traffic through the data center increases latency and degrades performance.  
( **Management Complexity** ) Fragmented, individual security solutions make unified policy management and visibility difficult.

## II. Mechanism & Components

### SASE Components and Technology Elements

```mermaid
flowchart LR
    U1["Remote User"] --> EDGE
    U2["Branch Office"] --> EDGE
    U3["Mobile Device"] --> EDGE

    EDGE["SASE\nCloud Edge"] --> NET["SD-WAN\nIntelligent Path Selection"]
    EDGE --> SEC["SSE Security Services\nZTNA / CASB / SWG"]

    NET --> R1["Public Cloud\nAWS / Azure / GCP"]
    SEC --> R2["SaaS Apps\nMicrosoft 365, etc."]
    NET --> R3["Data Center\nOn-Premises"]
```

> **Key Point**: The combination of networking technology that optimizes network paths with security technology that protects data and access.

### Key Components in Detail

| Category | Core Technology | Detailed Description |
|------|-------------|---------|
| Network (SD-WAN) | Software-Defined Wide Area Network | Intelligent, application-level path selection and ensured traffic availability |
| Security (SSE) | ZTNA | Zero-trust-based access control |
| Security (SSE) | CASB | Cloud app visibility and control |
| Security (SSE) | SWG | Secure web access and malware blocking |

## III. Advanced Topics & Comparison

### SASE vs. the Traditional Network Security Model

| Comparison | Traditional Model (Hub-and-Spoke) | SASE (Cloud Native) |
|----------|--------------------------|---------------------|
| Network Structure | Routed through the data center (backhauling) | Direct connection to the cloud edge |
| Security Services | Appliance-based (hardware) | Cloud-service-based (SaaS) |
| Manageability | Each solution managed separately (complex) | Unified single-policy management (simple) |
| Performance/Latency | High likelihood of bottlenecks | Low latency via distributed edge nodes |

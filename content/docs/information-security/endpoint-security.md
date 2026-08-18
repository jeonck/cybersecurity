---
weight: 1230
title: "Endpoint Security"
description: "The host-based security strategy that detects, blocks, and responds to threats once they reach an end-user device, at the front line beyond perimeter defenses."
icon: "devices"
date: "2026-08-18"
lastmod: "2026-08-18"
draft: false
---

## I. Overview

```mermaid
%%{init: { 'theme': 'base', 'themeVariables': { 'edgeLabelBackground': '#fff' }}}%%
flowchart LR
    A["Perimeter\nsecurity"] -- "Direct protection of the end device" --> B["Endpoint\nsecurity (node)"]
    style A fill:#f9f9f9,stroke:#333,stroke-width:3px
    style B fill:#e1f5fe,stroke:#01579b,stroke-width:3px
```

**Definition**: A host-based security strategy that detects, blocks, and responds to threats that have penetrated the network and reached an end-user device.

**Why It Is Needed**:  
( **Perimeter Collapse** ) The traditional network perimeter security model has been undermined by the shift to cloud and the spread of remote work  
( **Spread of BYOD** ) Increasing use of personal devices for work (**BYOD**) exposes unauthorized devices and endpoint vulnerabilities  
( **Advancing Threats** ) Advanced persistent threats (**APT**) and ransomware increasingly use end-user devices as their primary attack foothold  

## II. Mechanism & Components

### A. Evolution of Security Solutions and Gaining Visibility

```mermaid
flowchart LR
    EPP["EPP\n(Endpoint Protection Platform)\nsignature-based blocking\nfirst line of defense · antivirus"] -->|"Evolution"| EDR["EDR\n(Endpoint Detection & Response)\nreal-time behavioral log collection\ntracks unknown threats"]
    EDR -->|"Expansion"| XDR["XDR\n(Extended Detection & Response)\nendpoint + network + cloud\nunified detection and response"]
    EPP & EDR -->|"Unified management"| UEM["UEM\n(Unified Endpoint Management)\nunified PC + mobile management\napplies security policy uniformly"]
```

### B. Detailed Comparison of Key Security Functions

| Category | Key Technology | Description | Security Value |
|-----|---------|---------|-----------|
| Blocking | NGAV (Next-Gen Antivirus) | AI/machine-learning-based anomalous behavior detection | Defends against non-signature-based attacks |
| Detection | Behavioral Analysis | Tracks behavior such as file execution and registry modification | Detects zero-day attacks |
| Control | DLP (Data Loss Prevention) | Controls removable media, prevents screen capture, blocks file exfiltration | Prevents leakage of internal information |
| Management | Patch Management | Automates OS and application security updates | Removes vulnerabilities |

## III. Advanced Topics & Comparison

```mermaid
flowchart TD
    EP["Endpoint logs\n(EDR)"] --> XDR["XDR platform\nunified analysis engine"]
    NW["Network logs\n(NDR)"] --> XDR
    CL["Cloud logs\n(CASB / CSPM)"] --> XDR

    XDR -->|"Correlation analysis"| ATK["Full attack path\n(attack chain) identified"]
    ATK -->|"Threat confirmed"| AUTO["Automated response\nisolate · remediate · alert"]
    AUTO -->|"Integration"| SOAR["SOAR\nreduces response time"]
```

| Element | Description | Note |
|-----|---------|------|
| Data Integration | Unifies endpoint, network, and cloud logs into one place | Expands visibility |
| Correlation Analysis | Links fragmented events across layers to identify the full attack path | Cross-layer correlation |
| Automated Response | Automatically executes isolation and remediation when a threat is detected | Integrates with SOAR and cuts response time |

> **Key point**: XDR is a next-generation, unified security platform that extends EDR's endpoint visibility to the network and cloud, overcoming the limits of fragmented security solutions by tracking the entire kill chain in a single view.

---
weight: 10040
title: "OSSTMM (Open Source Security Testing Methodology Manual)"
description: "A security testing standard from ISECOM that scientifically and quantitatively measures the effectiveness of security controls to assess security maturity."
icon: "analytics"
date: "2026-08-18"
lastmod: "2026-08-18"
draft: false
---

## I. Overview

```mermaid
%%{init: { 'theme': 'base', 'themeVariables': { 'edgeLabelBackground': '#fff' }}}%%
flowchart LR
    A["Qualitative security assessment\nreliant on assessor judgment"] -- "Demand for a scientific method and\na quantitative security metric (RAV)" --> B["A measurable security\nstandard (OSSTMM)"]
    style A fill:#f9f9f9,stroke:#333,stroke-width:3px
    style B fill:#e1f5fe,stroke:#01579b,stroke-width:3px
```

**Definition**: A security testing standard developed by **ISECOM** (Institute for Security and Open Methodologies) that scientifically and quantitatively measures the effectiveness of security controls in order to assess an organization's security maturity.

**Features**:  
( **Quantitative Metric** ) Objectively quantifies security posture through a numeric value called the **RAV** (Risk Assessment Value), supporting executive decision-making.  
( **Scientific Methodology** ) Divides the target of testing into five operational channels and applies a consistent verification process to each.  
( **Comprehensive Scope** ) Goes beyond simple technical checks, performing an integrated assessment that covers human, physical, and wireless security as well.  
( **Open Source Standard** ) A transparent standard continuously updated by security experts worldwide, providing globally trusted security assurance.

## II. Mechanism & Components

### A. The Five Operational Channels of Security Testing

```mermaid
graph TD
    A["OSSTMM Operational Channels"] --> B["Data\n(Data Networks)"]
    A --> C["Human\nSecurity"]
    A --> D["Physical\nSecurity"]
    A --> E["Telecommunications\nSecurity"]
    A --> F["Wireless\nSecurity"]

    style B fill:#e3f2fd,stroke:#1e88e5
    style C fill:#fff3e0,stroke:#fb8c00
    style D fill:#f1f8e9,stroke:#7cb342
    style E fill:#fce4ec,stroke:#d81b60
    style F fill:#f3e5f5,stroke:#8e24aa
```

### B. Key Analytical Concepts and Process Characteristics

| Key Concept | Detailed Description | Security Value |
|:---:|----------|----------|
| **RAV** | **Risk Assessment Value** | Calculates the actual effectiveness of security controls ( **Security Actual** ) as a value between 0 and 100 |
| **Porosity** | The weaknesses (openings) through which the interior of a system can be penetrated | Measures the degree of external exposure and attack likelihood |
| **Separation** | The level of separation and independence between security controls | Verifies the effectiveness of **Defense in Depth** |
| **Limitations** | The inherent limits present within a security system | Identifies residual risk and informs response strategy |

## III. Comparison by Type & Selection Criteria

### A. Comparison of Major Security Methodologies

| Comparison | PTES (Execution Standard) | OSSTMM (Methodology Manual) |
|:---:|--------------------------|----------------------------|
| **Primary Goal** | **Standardizing the execution stages** of penetration testing | **Scientific/quantitative measurement** of security controls |
| **Output Format** | Focused on a technical vulnerability report | A statistical report based on the **RAV** metric |
| **Assessment Perspective** | Whether penetration succeeded (attacker's view) | Operational effectiveness of security controls (defender's view) |
| **Strength** | Concrete hacking technique guidelines | Quantitative figures suitable for executive reporting |

Don't treat this as an either/or choice — the two frameworks answer different questions for different audiences. Pull PTES's phase structure to actually run and manage the engagement day to day, and pull OSSTMM's RAV scoring for the moment the report reaches a CFO or board member who needs a trend line, not a stack of CVSS numbers. Most mature security programs end up running both side by side: PTES for process discipline, OSSTMM for the metric that survives translation to a non-technical audience.

### B. Selection Criteria by Program Maturity
- **Early-stage program, first pentest**: Start with PTES-style execution discipline — the priority is getting a consistent, defensible process in place before worrying about quantified trend reporting.
- **Established program, executive reporting needs**: Layer OSSTMM's RAV metric on top once the process is stable, so leadership can track security maturity numerically year over year instead of reading disconnected point-in-time reports.
- **Regulated or compliance-heavy environment**: Use OSSTMM's channel-based scope (human, physical, wireless, data) as objective evidence for certifications like **ISMS-P** and **ISO 27001** that explicitly require measuring maturity, not just listing findings.

> **Key Point**: The choice between PTES and OSSTMM is really a choice about audience — pick PTES when the deliverable's job is guiding remediation, pick OSSTMM when the deliverable's job is proving security maturity to people who don't read vulnerability reports.

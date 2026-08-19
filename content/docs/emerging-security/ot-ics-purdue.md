---
weight: 11040
title: "OT/ICS Security and the Purdue Model"
description: "A layered security framework built on the Purdue Model to protect operational technology and industrial control systems from cyber threats."
icon: "precision_manufacturing"
date: "2026-08-18"
lastmod: "2026-08-18"
draft: false
---

## I. Overview

```mermaid
%%{init: { 'theme': 'base', 'themeVariables': { 'edgeLabelBackground': '#fff' }}}%%
flowchart LR
    A["Air-gapped network\nClosed network"] -- "Growing IT/OT convergence\nand connectivity" --> B["Layered defense\nPurdue Model"]
    style A fill:#f9f9f9,stroke:#333,stroke-width:3px
    style B fill:#e1f5fe,stroke:#01579b,stroke-width:3px
```

**Definition**: A security framework for protecting the operational technology ( **OT** ) and industrial control systems ( **ICS** ) that run national infrastructure and industrial processes — manufacturing, energy, transportation, and more — from cyber threats.

**Features**:  
( **Availability first** ) Unlike IT security, which prioritizes confidentiality, OT security's top priority is uninterrupted, 24/7 operation and service continuity ( **Availability** ).  
( **Safety-centric** ) Because a cyberattack can translate directly into a physical accident, ensuring the safety ( **Safety** ) of people and equipment is essential.  
( **Limits of the air gap** ) To respond to the breakdown of air-gapped environments, layered network segmentation and control based on the **Purdue** model is applied.

## II. Mechanism & Components

### Purdue Model-Based OT/ICS Network Structure

```mermaid
flowchart TD
    L5["Level 4-5\nEnterprise IT\nCorporate network / external internet"]
    IDMZ["Level 3-3.5\nIndustrial DMZ (IDMZ)\nIT to OT isolation zone"]
    L2["Level 1-2\nControl\nPLC / SCADA / HMI"]
    L0["Level 0\nProcess\nSensor / Actuator"]

    L5 <-->|"NGFW\nfirewall"| IDMZ
    IDMZ <-->|"Unidirectional gateway\nprotocol conversion"| L2
    L2 <-->|"Physical access control"| L0
```

> **Key point**: Layers are separated from Level 0 (field devices) up to Level 5 (enterprise network), with the **Industrial DMZ (IDMZ)** isolating the IT and OT segments.

### Components and Security Measures by Level

| Level | Name and Components | Key Security Measures |
|:-----------:|----------------|------------------|
| Level 4-5 | Enterprise (IT) | Corporate network and external connectivity segment; apply next-generation firewalls (NGFW) |
| Level 3-3.5 | Site Operations (IDMZ) | Intermediate buffer zone; patch management servers, data replication, strengthened authentication |
| Level 1-2 | Control (PLC, SCADA) | Control-loop segment; whitelist-based intrusion detection, protocol inspection |
| Level 0 | Process (Sensor/Actuator) | Field physical devices; physical access control and monitoring for equipment anomalies |

## III. Adoption Considerations

| Risk | Mitigation |
|---|---|
| Vendor-specific industrial protocols (Modbus, S7, EtherNet/IP) evade generic IT security tools | Deep packet inspection (DPI) tuned to industrial protocols |
| Air-gap assumption broken by USB drives, maintenance laptops, or remote vendor access | Zero-trust device authentication at the point of connection, not just at the network perimeter |
| Inconsistent security baseline across vendors and integrators | Governance and certification under IEC 62443 |

Most OT breaches attributed to "the air gap failed" actually trace back to a maintenance laptop or USB drive that was trusted simply because it was physically present on-site. The fix isn't a tighter perimeter — it's authenticating every device at the point of connection, regardless of how it got there. Treat physical proximity to a Level 0/1 asset as zero evidence of trustworthiness.

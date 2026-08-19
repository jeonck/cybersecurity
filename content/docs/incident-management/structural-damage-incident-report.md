---
weight: 6050
title: "Structural Damage Incident Report"
description: "A facilities-owned template for documenting physical damage to buildings, equipment, or infrastructure and the resulting corrective actions."
icon: "domain_disabled"
date: "2026-08-18"
lastmod: "2026-08-18"
draft: false
---

## I. Overview

```mermaid
%%{init: { 'theme': 'base', 'themeVariables': { 'edgeLabelBackground': '#fff' }}}%%
flowchart LR
    A["Facilities damage handled\nverbally with no paper trail"] -- "Need for insurance, safety, and IT-impact documentation" --> B["Formal Structural Damage\nIncident Report"]
    style A fill:#f9f9f9,stroke:#333,stroke-width:3px
    style B fill:#e1f5fe,stroke:#01579b,stroke-width:3px
```

**Definition**: The Structural Damage Incident Report documents physical damage to a building, data center, or piece of infrastructure — from a leak or fire to storm or equipment-related damage — and the immediate and corrective actions taken.

**Features**:  
( **Ownership** ) Owned by facilities management, with IT security looped in whenever the damaged area houses servers, network equipment, or physical access-control systems.  
( **Insurance & Compliance** ) Supports insurance claims and safety compliance documentation.  
( **IT Impact** ) Ensures damage affecting IT infrastructure triggers the appropriate availability and data-integrity response.  
( **Coordinated Response** ) Aligns the physical repair with any needed IT security response.

## II. Structure & Process

```mermaid
flowchart TD
    D["Damage discovered"] --> L["Facilities logs report"]
    L --> S{"Safety risk or IT impact?"}
    S -- "Safety risk" --> Evac["Evacuate and secure area"]
    S -- "IT impact" --> ITSec["Loop in IT security / infrastructure team"]
    S -- "Neither" --> Assess["Assess and schedule repair"]
    Evac --> Assess
    ITSec --> Assess
    Assess --> Repair["Repair and restore"]
    Repair --> Close["Close report with insurance/compliance notes"]
```

| Field | Description |
|---|---|
| Location & Date | Building, room, or facility affected and when the damage was discovered |
| Damage Type | Category, e.g. water, fire, structural collapse, storm, equipment failure |
| Reported By | Individual who first identified or reported the damage |
| Severity & Safety Risk | Assessment of whether the area is safe to occupy or requires evacuation |
| IT / Infrastructure Impact | Whether servers, network gear, or access-control systems are affected |
| Immediate Action | Steps taken to secure the area and prevent further damage |
| Repair & Restoration Plan | Vendor, timeline, and cost estimate for remediation |
| Insurance / Compliance Notes | Claim reference and any regulatory notifications required |

Facilities logs the report within hours of discovery, and IT security is notified immediately if the affected area houses infrastructure or physical access controls.

## III. Comparison & Application

| Report Type | Use When | Owner |
|---|---|---|
| Structural Damage Incident Report | Physical damage to a building or infrastructure, IT impact incidental | Facilities |
| [Major Incident Report Template](../major-incident-report-template/) | The damage takes down or exposes IT infrastructure as the primary concern | SOC / IR Team |
| [Workplace Violence Report](../workplace-violence-report/) | The event involves a person's conduct rather than the facility itself | HR / Security |

The deciding factor is which risk is primary, not which one is merely present — a server-room flood is a Structural Damage report with an IT-impact field filled in if the servers were only at risk, but it graduates to a Major Incident Report the moment data availability or integrity is actually compromised. Facilities and IT security should agree on that threshold in advance, not while standing in a flooded server room deciding who owns the write-up.

Related: [Major Incident Report Template](../major-incident-report-template/), [Incident Management Process](../incident-management-process/)

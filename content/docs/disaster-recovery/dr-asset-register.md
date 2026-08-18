---
weight: 820
title: "DR Asset Register"
description: "A maintained inventory mapping systems and infrastructure to criticality tier, dependencies, and recovery targets."
icon: "inventory_2"
date: "2026-08-18"
lastmod: "2026-08-18"
draft: false
---

## I. Overview

```mermaid
%%{init: { 'theme': 'base', 'themeVariables': { 'edgeLabelBackground': '#fff' }}}%%
flowchart LR
    A["Recovery plan referencing an\nuntracked, stale system list"] -- "Need accurate mapping of\nassets to recovery priority" --> B["Maintained DR Asset\nRegister"]
    style A fill:#f9f9f9,stroke:#333,stroke-width:3px
    style B fill:#e1f5fe,stroke:#01579b,stroke-width:3px
```

**Definition**: A DR Asset Register is the current, validated inventory of every system, application, and piece of infrastructure in scope for disaster recovery, mapped to its business owner, dependencies, criticality tier, and per-asset **RTO**/**RPO** targets.

**Features**:  
( **Ownership** ) Maintained by the IT infrastructure or asset management team in coordination with the DR coordinator.  
( **Foundational Role** ) Serves as the factual foundation every DR plan is sequenced against.  
( **Sequencing Risk** ) A DR plan built on a stale asset list recovers systems in the wrong order or misses undocumented dependencies.  
( **Data Integrity** ) A stale register can point recovery efforts at infrastructure that no longer exists.

## II. Structure & Process

| Field | Description |
|---|---|
| Asset/System Name | The application, database, or infrastructure component being tracked. |
| Business Owner | The individual or team accountable for the asset. |
| Criticality Tier | Recovery priority tier assigned per the DR Approach Document. |
| Dependencies | Upstream and downstream systems required for this asset to function. |
| Target RTO | Maximum acceptable downtime for this specific asset. |
| Target RPO | Maximum acceptable data loss for this specific asset. |
| Recovery Site/Method | Where and how the asset is restored (hot site, cloud failover, backup restore). |
| Last Validated Date | Date the entry was last confirmed accurate against the live environment. |

```mermaid
sequenceDiagram
    participant Owner as "Asset/System Owner"
    participant Coordinator as "DR Coordinator"
    participant Register as "DR Asset Register"
    participant Plan as "DR Plan Template"

    Owner->>Coordinator: "Report new or changed system"
    Coordinator->>Register: "Update entry with tier, RTO/RPO, dependencies"
    Coordinator->>Plan: "Feed prioritized asset list into recovery plan"
    Coordinator->>Register: "Reconcile against CMDB on fixed cadence"
```

## III. Best Practices & Comparison

| Document | Primary Purpose | When Used | Owner |
|---|---|---|---|
| DR Asset Register | Track which assets exist and their recovery priority | Continuously maintained, discovery-driven | IT infrastructure/asset management |
| DR Plan Template | Provide step-by-step recovery procedures per system | Built from register data; invoked during a disaster | System/application owners, DR coordinator |
| DR Approach Document | Define criticality tiers and recovery strategy options | Set once, revisited periodically | DR coordinator, IT/security leadership |

- Reconcile the register against the CMDB or cloud asset inventory on a fixed cadence, not only before an exercise.
- Record dependencies explicitly — a missed dependency is the most common cause of a failed recovery sequence.
- Assign every asset a business owner accountable for confirming its criticality tier and recovery targets.
- Treat an unvalidated entry older than the review cadence as untrustworthy until re-confirmed.

Related: [DR Plan Template](../dr-plan-template/), [DR Approach Document](../dr-approach-document/). See also [Cloud Backup & Recovery Testing Tracker](/docs/cloud-security/cloud-backup-recovery-testing-tracker/) for cloud-specific restore validation.

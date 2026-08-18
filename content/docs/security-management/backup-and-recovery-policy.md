---
weight: 530
title: "Backup and Recovery Policy"
description: "Establishes requirements for data backup frequency, retention, testing, and restoration to protect against data loss."
icon: "backup"
date: "2026-08-18"
lastmod: "2026-08-18"
draft: false
---

## I. Overview

A Backup and Recovery Policy defines what data must be backed up, how often, where copies are stored, and how restoration is tested and executed. It is jointly owned by IT operations, who run the backups, and the CISO or GRC team, who set the risk-driven requirements. Without a formal policy, backup coverage tends to drift — some systems are backed up inconsistently or not at all — and organizations only discover the gap during an actual incident, when it is too late to correct.

```mermaid
%%{init: { 'theme': 'base', 'themeVariables': { 'edgeLabelBackground': '#fff' }}}%%
flowchart LR
    A["Ad-hoc, unverified system backups"] -- "Need for guaranteed recovery within defined limits" --> B["Formal Backup and Recovery Policy"]
    style A fill:#f9f9f9,stroke:#333,stroke-width:1px
    style B fill:#e1f5fe,stroke:#01579b,stroke-width:1px
```

## II. Structure & Process

| Field | Description |
|---|---|
| Scope of Systems | Which systems and data stores are covered, prioritized by business criticality. |
| Backup Frequency | How often backups run — continuous, daily, weekly — per system tier. |
| Recovery Point Objective (RPO) | Maximum acceptable data loss, measured in time, per system. |
| Recovery Time Objective (RTO) | Maximum acceptable downtime before restoration, per system. |
| Retention Period | How long backup copies are kept before rotation or deletion. |
| Storage & Offsite Requirements | Onsite vs. offsite/cloud copies, encryption at rest, and geographic separation. |
| Restoration Testing | Frequency and method of test restores to validate backup integrity. |
| Incident Escalation | Who authorizes and executes a restoration during an active incident. |

```mermaid
sequenceDiagram
    participant IT as "IT Operations"
    participant Security as "Security/GRC Team"
    participant Committee as "ISMS Steering Committee"
    participant Auditor as "Internal Audit"

    IT->>Security: "Propose backup schedule and RPO/RTO targets"
    Security->>Committee: "Submit policy for approval"
    Committee->>IT: "Approve and mandate testing cadence"
    IT->>IT: "Run scheduled test restorations"
    IT->>Auditor: "Provide test-restore evidence for review"
```

IT operations proposes technical parameters, security/GRC validates them against business impact analysis, and the ISMS steering committee approves the policy. Test restorations are logged as evidence and reviewed by internal audit; the policy itself is reviewed annually or after any recovery failure.

## III. Best Practices & Comparison

| Document | Primary Purpose | Review Cadence | Owner |
|---|---|---|---|
| Backup and Recovery Policy | Guarantee recoverability of data and systems | Annual | IT operations, CISO / GRC team |
| Information Classification Policy | Define sensitivity tiers that drive backup encryption needs | Annual or on data inventory change | Data owners, security team |
| ISMS Policy | Set the overarching management-system framework | Annual | CISO |

- Set RPO/RTO per system tier based on business impact, not a single blanket target for everything.
- Test restorations on a fixed schedule; an untested backup is an unverified assumption.
- Keep at least one backup copy offsite or air-gapped to survive ransomware that targets connected backups.
- Encrypt backup data at rest and in transit, especially for offsite and cloud copies.
- Document and rehearse the restoration escalation path so recovery isn't improvised during an incident.

Related: [ISMS Policy](../isms-policy/), [Disposal and Destruction Policy](../disposal-and-destruction-policy/).

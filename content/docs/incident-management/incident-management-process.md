---
weight: 620
title: "Incident Management Process"
description: "The operational, step-by-step procedure the SOC and IR team follow from detection through resolution and post-incident review."
icon: "sync_alt"
date: "2026-08-18"
lastmod: "2026-08-18"
draft: false
---

## I. Overview

```mermaid
%%{init: { 'theme': 'base', 'themeVariables': { 'edgeLabelBackground': '#fff' }}}%%
flowchart LR
    A["Ad-hoc verbal\nincident handoffs"] -- "Need for consistent triage and accountability" --> B["Formal Incident\nManagement Process"]
    style A fill:#f9f9f9,stroke:#333,stroke-width:3px
    style B fill:#e1f5fe,stroke:#01579b,stroke-width:3px
```

**Definition**: The Incident Management Process is the operational runbook that translates the Incident Management Policy into concrete, repeatable steps: how an event is detected, logged, triaged, escalated, contained, and closed out.

**Features**:  
( **Ownership** ) Owned and executed by the SOC / incident response team.  
( **Telemetry** ) SIEM and EDR platforms provide the detection and telemetry that feed the process.  
( **Consistency** ) Replaces inconsistent, memory-based handling that extends dwell time and loses forensic evidence.  
( **Audit Readiness** ) Produces incident records detailed enough to support root-cause analysis and compliance audits.

## II. Structure & Process

| Field | Description |
|---|---|
| Detection Source | Origin of the alert, e.g. **SIEM** correlation rule, **EDR** behavioral alert, user report |
| Incident ID | Unique tracking number assigned at logging for chain-of-custody and reporting |
| Severity Level | Tier assigned during triage per the governing policy |
| Assigned Responder | Analyst or incident commander responsible for the response |
| Containment Action | Immediate step taken to limit spread (isolate host, disable account, block IP) |
| Timeline | Timestamped sequence of detection, triage, containment, and resolution events |
| Root Cause | Underlying technical or process failure identified during investigation |
| Corrective Action | Follow-up remediation or control change to prevent recurrence |

```mermaid
sequenceDiagram
    participant SIEM as "SIEM / EDR"
    participant Analyst as "SOC Analyst"
    participant IC as "Incident Commander"
    participant Team as "IR Team"

    SIEM->>Analyst: "Raise alert"
    Analyst->>Analyst: "Log incident and gather initial evidence"
    Analyst->>IC: "Triage and assign severity"
    IC->>Team: "Escalate and assign containment tasks"
    Team->>Team: "Contain, eradicate, and recover"
    Team->>IC: "Report resolution"
    IC->>Analyst: "Conduct post-incident review"
```

Every incident record is closed only after root cause and corrective actions are documented, and high-severity incidents proceed to a formal post-incident review meeting.

## III. Best Practices & Comparison

| Document | Primary Purpose | Trigger | Owner |
|---|---|---|---|
| Incident Management Process | Step-by-step operational handling of any incident | Any detected event | SOC / IR Team |
| [Incident Management Policy](../incident-management-policy/) | Governance rules and definitions behind the process | Annual review or policy gap | CISO / Executive Management |
| [Major Incident Report Template](../major-incident-report-template/) | Detailed record of a single high-severity incident | Critical or high-severity event | SOC / IR Team |

- Preserve volatile evidence (memory, session state, logs) before containment actions destroy it.
- Maintain a timestamped timeline in real time rather than reconstructing it after the fact.
- Route every incident through the same intake queue so nothing is triaged informally outside the process.
- Hold a blameless post-incident review for every medium-or-higher severity incident.
- Feed corrective actions back into detection rules (SIEM/EDR) to close the loop on recurring root causes.

Related: [Incident Management Policy](../incident-management-policy/), [Major Incident Report Template](../major-incident-report-template/)

---
weight: 6020
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

Every incident record is closed only after root cause and corrective actions are documented, and high-severity incidents proceed to a formal post-incident review meeting.

## III. Adoption Considerations

| Risk | Primary Control |
|---|---|
| Volatile evidence lost during containment | Capture memory / session state before isolating or rebuilding a host |
| Inconsistent handling outside the process | Single intake queue for every incident, no informal side-channel triage |
| Corrective actions never close the loop | Feed root-cause findings back into SIEM/EDR detection rules, not just the retro notes |

The step teams skip under pressure is almost always evidence preservation before containment — isolating a compromised host feels like the responsible move in the moment, but it also destroys the memory-resident indicators that would have explained how the attacker got in. Build "capture before contain" into the runbook itself rather than leaving it to responder judgment, because judgment is exactly what's compromised at 2 a.m. during a live incident.

Related: [Incident Management Policy](../incident-management-policy/), [Major Incident Report Template](../major-incident-report-template/)

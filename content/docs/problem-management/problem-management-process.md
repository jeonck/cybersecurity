---
weight: 7030
title: "Problem Management Process"
description: "The end-to-end ITIL workflow for turning recurring incidents into diagnosed problems, known errors, and permanent fixes."
icon: "sync_alt"
date: "2026-08-18"
lastmod: "2026-08-18"
draft: false
---

## I. Overview

```mermaid
%%{init: { 'theme': 'base', 'themeVariables': { 'edgeLabelBackground': '#fff' }}}%%
flowchart LR
    A["Ad-hoc, inconsistent handling\nof recurring incidents"] -- "Need a repeatable path from symptom to root-cause fix" --> B["Documented Problem\nManagement Process"]
    style A fill:#f9f9f9,stroke:#333,stroke-width:3px
    style B fill:#e1f5fe,stroke:#01579b,stroke-width:3px
```

**Definition**: The Problem Management Process defines how an organization moves from a pattern of incidents to a diagnosed root cause to a permanent fix, in a repeatable, auditable way.

**Features**:  
( **Ownership** ) Owned by the problem manager as a process document.  
( **Reference Use** ) Referenced by service desk, incident response, and engineering teams whenever incidents recur or a single incident warrants investigation.  
( **ITIL Distinction** ) Enforces the ITIL split between incident management, optimized for speed of restoration, and problem management, optimized for permanence of resolution.  
( **Trade-off** ) Deliberately trades immediate closure for durable prevention of the root cause.

## II. Structure & Process

```mermaid
flowchart LR
    A["Problem identification"] --> B["Problem logging"]
    B --> C["Categorization and prioritization"]
    C --> D["Root cause analysis"]
    D --> E["Known Error Record published"]
    E --> F["Permanent fix via change management"]
    F --> G["Resolution verified"]
    G --> H["Problem closure"]
```

| Field | Description |
|---|---|
| Process Stage | Named phase, e.g. identification, logging, categorization, diagnosis. |
| Entry Criteria | Condition that triggers the stage, such as recurrence threshold. |
| Key Activities | Actions performed by the problem manager or investigation team. |
| Roles Involved | Service desk, problem manager, technical SMEs, security team. |
| Exit Criteria | Deliverable required to advance, e.g. confirmed root cause. |
| Supporting Records | Problem Record, Known Error Record, or Major Problem Report produced. |

Problems are identified either proactively, through trend analysis of incident data, or reactively, from a single major incident; both paths converge on the same logging, diagnosis, and closure stages so every problem is tracked with equal rigor regardless of origin.

## III. Expected Benefits & Implications

A formal problem management process is often the easiest line item to cut, because in a quiet quarter it looks like documentation layered on top of incident response that already restored everything. The payoff is uneven by design — most incidents never touch this process, but the recurring ones that do would otherwise consume the same on-call hours over and over with nothing to show for it.

| Benefit | Where It Shows Up |
|---|---|
| Falling repeat-incident rate | Incident trend reports, month over month |
| Faster diagnosis on recurrence | Known Error Records reused instead of re-investigated |
| Defensible root-cause evidence | Security and audit reviews of recurring exposure |
| Bounded investigation backlog | Explicit exit criteria per stage, not open-ended tickets |

Measure the process by the trend in repeat-incident rate, not by problem-record volume — a team can log plenty of problem records and still leave the same root causes unfixed. The more durable implication is organizational: feeding a security incident's confirmed root cause into this process, rather than closing it purely within incident response, is what turns a one-off patch into a documented, auditable decision that survives staff turnover.

Related: [Problem Record Template](../problem-record-template/), [Known Error (KE) Record Template](../known-error-record-template/), [Major Problem Report Template](../major-problem-report-template/).

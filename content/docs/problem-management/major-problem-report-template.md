---
weight: 720
title: "Major Problem Report Template"
description: "A formal post-resolution review of a high-impact problem's root cause, resolution, and lessons learned."
icon: "assessment"
date: "2026-08-18"
lastmod: "2026-08-18"
draft: false
---

## I. Overview

```mermaid
%%{init: { 'theme': 'base', 'themeVariables': { 'edgeLabelBackground': '#fff' }}}%%
flowchart LR
    A["Major problem closed\nwith no formal review"] -- "Need to capture cost, cause, and lessons for leadership" --> B["Major Problem\nReport"]
    style A fill:#f9f9f9,stroke:#333,stroke-width:3px
    style B fill:#e1f5fe,stroke:#01579b,stroke-width:3px
```

**Definition**: A Major Problem Report is the formal, executive-facing review produced after a high-impact or high-recurrence problem has been resolved (or requires escalated attention).

**Features**:  
( **Ownership** ) Owned by the problem manager, typically with sign-off from service owners and, for security-rooted problems, the CISO.  
( **Root-Cause Focus** ) Explains why the fault existed in the first place, where an incident report explains only how service was restored.  
( **Cost Accounting** ) Captures what the problem cost across every recurrence, not just the final incident.  
( **Structural Change** ) Documents what structural changes prevent the problem happening again, turning a technical fix into an organizational lesson.

## II. Structure & Process

| Field | Description |
|---|---|
| Report ID | Unique identifier linking the report to the source Problem Record. |
| Executive Summary | Plain-language description of the problem, impact, and outcome. |
| Root Cause Analysis | Detailed technical findings, including analysis method used. |
| Business/Security Impact | Cumulative cost across recurrences: downtime, data exposure, revenue. |
| Timeline | Key dates from first occurrence through permanent resolution. |
| Resolution Summary | Permanent fix delivered and how it was validated. |
| Lessons Learned | Process, tooling, or design gaps identified during review. |
| Follow-Up Actions | Preventive actions with owners and target dates. |

```mermaid
flowchart TD
    A["Major problem identified and prioritized"] --> B["Root cause analysis completed"]
    B --> C["Known error and workaround published"]
    C --> D["Permanent fix implemented and verified"]
    D --> E["Major Problem Report drafted"]
    E --> F["Review with stakeholders and leadership"]
    F --> G["Follow-up preventive actions tracked to completion"]
```

Drafting begins once the permanent fix is verified, and the report is finalized after stakeholder review confirms the root cause, impact figures, and follow-up actions are accurate and assigned.

## III. Best Practices & Comparison

| Document | Primary Purpose | Trigger | Owner |
|---|---|---|---|
| Major Problem Report Template | Formal post-resolution review with impact and lessons learned | Major problem resolved or under executive review | Problem manager / service owner |
| Problem Record Template | Working record of investigation from open to closed | Recurring or significant incident pattern | Problem manager |
| Major Incident Report Template | Document how a single major incident was detected and restored | Major incident declared | Incident commander |

- Quantify cumulative impact across all recurrences, not just the triggering incident, to justify remediation investment.
- Separate root cause from contributing factors so the report does not overstate a single point of failure.
- Route follow-up actions through change management with named owners and dates, not open-ended commitments.
- Distinguish this report from a major incident report: incident response measures time-to-restore, problem review measures time-to-eliminate-cause.
- Circulate lessons learned beyond the immediate team so similar architectures elsewhere can be checked proactively.

Related: [Problem Record Template](../problem-record-template/), [Known Error (KE) Record Template](../known-error-record-template/), [Major Incident Report Template](/docs/incident-management/major-incident-report-template/).

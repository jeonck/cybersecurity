---
weight: 840
title: "DR Communications Plan"
description: "A predefined protocol for who communicates what, to whom, and through which channel during a declared disaster."
icon: "campaign"
date: "2026-08-18"
lastmod: "2026-08-18"
draft: false
---

## I. Overview

A DR Communications Plan defines, in advance, who notifies which stakeholder group during a declared disaster, through which channel, using which pre-approved message templates, and under what escalation timing. It is owned by the DR coordinator working with corporate communications and legal, and it is exercised alongside the DR Plan Template. Without it, teams improvise messaging under pressure while racing against **RTO** targets, which produces inconsistent or premature statements to staff, customers, or regulators — a failure mode distinct from, but as damaging as, missing a recovery deadline.

```mermaid
%%{init: { 'theme': 'base', 'themeVariables': { 'edgeLabelBackground': '#fff' }}}%%
flowchart LR
    A["Ad hoc, inconsistent messaging during past outages"] -- "Need a pre-approved, role-based communication protocol" --> B["Formal DR Communications Plan"]
    style A fill:#f9f9f9,stroke:#333,stroke-width:1px
    style B fill:#e1f5fe,stroke:#01579b,stroke-width:1px
```

## II. Structure & Process

| Field | Description |
|---|---|
| Stakeholder Group | Internal staff, executives, customers, regulators, or media. |
| Notification Trigger | The event or elapsed time that requires this group to be informed. |
| Channel | Email, SMS/paging, status page, press release, or direct call. |
| Message Template/Reference | Pre-approved wording or reference to the template library. |
| Responsible Communicator | Named role authorized to send the notification. |
| Approval Requirement | Whether legal or executive sign-off is required before sending. |
| Escalation Timing | Maximum time allowed between disaster declaration and first notification per group. |
| Regulatory/Legal Review Needed | Whether the event triggers mandatory disclosure obligations. |

```mermaid
sequenceDiagram
    participant IC as "Incident Commander"
    participant Comms as "Comms Lead"
    participant Staff as "Internal Staff"
    participant Exec as "Executives/Legal"
    participant External as "Customers/Regulators"

    IC->>Comms: "Declare disaster, activate communications plan"
    Comms->>Staff: "Send initial internal notification"
    Comms->>Exec: "Provide status briefing for approval"
    Comms->>External: "Send external notification if required"
    Comms->>Staff: "Issue stand-down notice at closure"
```

## III. Best Practices & Comparison

| Document | Primary Purpose | When Used | Owner |
|---|---|---|---|
| DR Communications Plan | Coordinate stakeholder messaging during the event | Activated alongside the DR plan on declaration | DR coordinator, corporate communications |
| DR Plan Template | Provide step-by-step recovery procedures per system | Built and tested before activation; executed during it | System/application owners, DR coordinator |
| DR Closure Report | Record recovery outcomes and drive corrective action | After every exercise or real activation | DR coordinator, steering committee |

- Pre-draft and legally review message templates before an event, not during one.
- Name a single responsible communicator per stakeholder group to prevent conflicting statements.
- Set explicit escalation timing so notification delay doesn't compound the outage itself.
- Rehearse the communications plan in tabletop exercises alongside the technical recovery steps, not as an afterthought.

Related: [DR Plan Template](../dr-plan-template/), [DR Closure Report](../dr-closure-report/). See also the [Incident Management](/docs/incident-management/) category for broader stakeholder notification practices.

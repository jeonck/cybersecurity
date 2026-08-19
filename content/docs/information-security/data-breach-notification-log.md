---
weight: 1020
title: "Data Breach Notification Log"
description: "A chronological record of confirmed breaches, notification decisions, and disclosure timelines used to demonstrate regulatory compliance."
icon: "report"
date: "2026-08-18"
lastmod: "2026-08-18"
draft: false
---

## I. Overview

```mermaid
%%{init: { 'theme': 'base', 'themeVariables': { 'edgeLabelBackground': '#fff' }}}%%
flowchart LR
    A["Informal incident notes\nscattered across email"] -- "Need to prove regulatory\nnotification timelines" --> B["Centralized Data Breach\nNotification Log"]
    style A fill:#f9f9f9,stroke:#333,stroke-width:3px
    style B fill:#e1f5fe,stroke:#01579b,stroke-width:3px
```

**Definition**: A Data Breach Notification Log is the authoritative record of confirmed data breaches: what happened, who was affected, which regulators or individuals were notified, and when.

**Features**:  
( **Ownership** ) Owned by the CISO or incident response lead, with input from legal/privacy counsel who determine notification obligations.  
( **Regulatory Window** ) Many breach notification regulations require disclosure to a supervisory authority within a tight window, commonly cited as 72 hours from confirmed discovery.  
( **Compliance Evidence** ) Exists to prove that timeline was met, or to explain any deviation, during a regulatory inquiry.

## II. Structure & Process

```mermaid
sequenceDiagram
    participant SOC as "Security Operations"
    participant IR as "Incident Response Lead"
    participant Legal as "Legal/Privacy Counsel"
    participant Regulator as "Regulatory Authority"

    SOC->>IR: "Confirm and escalate suspected breach"
    IR->>Legal: "Assess notification obligation and scope"
    Legal->>IR: "Determine required deadline and recipients"
    IR->>Regulator: "Submit notification within required window"
    IR->>IR: "Record all decisions and timestamps in log"
```

| Field | Description |
|---|---|
| Incident ID | Unique reference linking to the broader incident response record. |
| Discovery Date/Time | When the breach was first confirmed, which starts the notification clock. |
| Data Categories Affected | Types of data exposed, e.g. personal identifiers, financial, health. |
| Estimated Affected Individuals | Count or estimate of impacted data subjects. |
| Root Cause | Summary of how the breach occurred. |
| Regulatory Notification Status | Whether and when the relevant authority was notified. |
| Individual Notification Status | Whether and when affected individuals were informed. |
| Notification Deadline | Regulatory or contractual deadline applicable to the incident. |
| Remediation Actions | Containment and corrective steps taken. |

Entries are created the moment a breach is confirmed, updated continuously through containment and notification, and formally closed once all required disclosures are complete and remediation is verified.

## III. Implications & Recommendations

Treating breach notification as a legal deadline rather than a security control is the mistake that turns a bad week into a regulatory enforcement action — the log's real value is proving the clock started at confirmed discovery, not suspicion, and that every hour after was accounted for. Tabletop exercises that never touch this log are testing containment speed while ignoring the disclosure deadline regulators actually measure.

| Implication | Practical Effect | Time Horizon |
|---|---|---|
| Clean discovery timestamp | Withstands regulatory scrutiny on notification timing | Captured at time of confirmation |
| Legal counsel engaged early | Jurisdiction-specific obligations identified before deadline pressure builds | First 24-48 hours |
| Separation from general IR tickets | Regulatory evidence isn't buried in unrelated operational detail | Ongoing |

- Start the notification clock from confirmed discovery, not from initial suspicion, and document that timestamp precisely.
- Record regulator and individual notification separately, since deadlines and thresholds often differ.
- Review closed entries during tabletop exercises to validate that response times can meet stated deadlines.

Related: [Data Loss Prevention (DLP) Incident Log](../data-loss-prevention-incident-log/), [Data Classification Register](../data-classification-register/).

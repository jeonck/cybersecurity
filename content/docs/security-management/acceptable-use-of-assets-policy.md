---
weight: 510
title: "Acceptable Use of Assets Policy"
description: "Defines permitted and prohibited use of company-owned devices, accounts, and network resources by employees and contractors."
icon: "gavel"
date: "2026-08-18"
lastmod: "2026-08-18"
draft: false
---

## I. Overview

An Acceptable Use of Assets Policy (AUP) sets the rules for how employees, contractors, and third parties may use company-owned IT assets — laptops, mobile devices, email accounts, cloud storage, and network access. It is maintained by the CISO or IT security team and enforced jointly with HR, since violations can trigger disciplinary action. Organizations need a written AUP because informal expectations do not hold up in an audit, a legal dispute, or a termination-for-cause case; a signed policy gives the organization a documented basis for monitoring, restricting, and disciplining misuse.

```mermaid
%%{init: { 'theme': 'base', 'themeVariables': { 'edgeLabelBackground': '#fff' }}}%%
flowchart LR
    A["Unwritten, assumed norms for using company devices"] -- "Need for an enforceable, signed baseline" --> B["Formal Acceptable Use of Assets Policy"]
    style A fill:#f9f9f9,stroke:#333,stroke-width:1px
    style B fill:#e1f5fe,stroke:#01579b,stroke-width:1px
```

## II. Structure & Process

| Field | Description |
|---|---|
| Scope of Assets | Devices, accounts, and services covered — laptops, mobile devices, email, cloud storage, network access. |
| Permitted Use | Business use and reasonable incidental personal use, clearly bounded. |
| Prohibited Activities | Unauthorized software installation, unlicensed media, illegal content, harassment, personal commercial activity. |
| Monitoring & Privacy Notice | Statement that company assets and traffic may be logged, inspected, or monitored. |
| BYOD Provisions | Rules for personally owned devices accessing corporate data, if permitted. |
| Consequences of Violation | Disciplinary escalation path, up to termination and legal referral. |
| Acknowledgment Requirement | Signature or digital attestation required at onboarding and on policy update. |
| Exception Process | How a business unit requests a deviation, and who approves it. |

```mermaid
sequenceDiagram
    participant Security as "Security/GRC Team"
    participant HR as "HR"
    participant Committee as "ISMS Steering Committee"
    participant Employee as "Employee"

    Security->>HR: "Draft policy and align with disciplinary process"
    HR->>Committee: "Submit for review and approval"
    Committee->>Security: "Approve and set annual review cycle"
    Security->>Employee: "Distribute policy and collect acknowledgment"
    Employee->>Security: "Sign attestation at onboarding and on update"
```

The AUP is drafted by security with HR input, approved by the ISMS steering committee, and reissued for signature whenever materially revised — typically on an annual cycle or after a significant incident prompts a scope change.

## III. Best Practices & Comparison

| Document | Primary Purpose | Review Cadence | Owner |
|---|---|---|---|
| Acceptable Use of Assets Policy | Define permitted/prohibited use of company IT assets | Annual | CISO / GRC team |
| Password Policy | Set authentication strength requirements | Annual | CISO / GRC team |
| Information Classification Policy | Define sensitivity tiers for handling data | Annual or on data inventory change | Data owners, security team |

- Require signed acknowledgment at onboarding and after every material revision, not just once at hire.
- State the monitoring and privacy notice explicitly to avoid disputes over expectation of privacy.
- Keep prohibited-activity language specific enough to be enforceable, not just aspirational.
- Align disciplinary consequences with HR's existing progressive-discipline framework.
- Review annually and after any incident that exposes a gap in current asset-use rules.

Related: [Password Policy](../password-policy/), [Information Classification Policy](../information-classification-policy/).

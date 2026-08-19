---
weight: 5010
title: "Acceptable Use of Assets Policy"
description: "Defines permitted and prohibited use of company-owned devices, accounts, and network resources by employees and contractors."
icon: "gavel"
date: "2026-08-18"
lastmod: "2026-08-18"
draft: false
---

## I. Overview

```mermaid
%%{init: { 'theme': 'base', 'themeVariables': { 'edgeLabelBackground': '#fff' }}}%%
flowchart LR
    A["Unwritten, assumed norms\nfor using company devices"] -- "Need for an enforceable,\nsigned baseline" --> B["Formal Acceptable Use\nof Assets Policy"]
    style A fill:#f9f9f9,stroke:#333,stroke-width:3px
    style B fill:#e1f5fe,stroke:#01579b,stroke-width:3px
```

**Definition**: An Acceptable Use of Assets Policy (AUP) is the document that sets the rules for how employees, contractors, and third parties may use company-owned IT assets — laptops, mobile devices, email accounts, cloud storage, and network access.

**Features**:  
( **Ownership** ) Maintained by the CISO or IT security team and enforced jointly with HR, since violations can trigger disciplinary action.  
( **Audit Basis** ) Gives the organization a documented basis for monitoring, restricting, and disciplining misuse.  
( **Legal Standing** ) Holds up in an audit, a legal dispute, or a termination-for-cause case where informal expectations would not.  
( **Scope** ) Covers company-owned devices, accounts, cloud storage, and network access across employees and third parties.

## II. Structure & Process

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

The AUP is drafted by security with HR input, approved by the ISMS steering committee, and reissued for signature whenever materially revised — typically on an annual cycle or after a significant incident prompts a scope change.

## III. Expected Benefits & Implications

The AUP's payoff rarely shows up in day-to-day operations — it shows up the one time a termination-for-cause decision gets challenged, or a regulator asks how misuse was even detected. An unsigned, informal expectation carries no weight in that conversation; a dated attestation does.

| Benefit | Where It Shows Up |
|---|---|
| Defensible termination decisions | HR and legal disputes over disciplinary action |
| Documented monitoring basis | Regulatory inquiries, privacy disputes |
| Reduced insider-misuse exposure | Fewer unauthorized software and data incidents |
| Faster onboarding and offboarding | Standardized rules instead of case-by-case judgment |

Treat the signed acknowledgment as the actual deliverable, not the policy document itself — an AUP nobody signed is a draft, not a control, no matter how well it reads.

Related: [Password Policy](../password-policy/), [Information Classification Policy](../information-classification-policy/).

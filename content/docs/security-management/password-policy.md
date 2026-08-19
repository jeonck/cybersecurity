---
weight: 5020
title: "Password Policy"
description: "Sets enforceable minimum standards for password strength, rotation, storage, and multi-factor authentication across systems."
icon: "password"
date: "2026-08-18"
lastmod: "2026-08-18"
draft: false
---

## I. Overview

```mermaid
%%{init: { 'theme': 'base', 'themeVariables': { 'edgeLabelBackground': '#fff' }}}%%
flowchart LR
    A["Informal, unwritten\npassword expectations"] -- "Need for enforceable,\nauditable minimum standards" --> B["Formal Password\nPolicy"]
    style A fill:#f9f9f9,stroke:#333,stroke-width:3px
    style B fill:#e1f5fe,stroke:#01579b,stroke-width:3px
```

**Definition**: A Password Policy is the document that defines the minimum authentication standards employees and systems must meet — length, complexity, rotation, reuse restrictions, and where multi-factor authentication (MFA) is mandatory.

**Features**:  
( **Ownership** ) Maintained by the CISO or IT security team and technically enforced through identity and access management (IAM) tooling and directory services.  
( **Breach Prevention** ) Closes off weak or reused credentials, one of the most common initial-access vectors in breaches.  
( **Regulatory Baseline** ) Gives regulators and auditors a documented baseline rather than per-system, ad hoc rules.  
( **MFA Requirements** ) Specifies where multi-factor authentication is mandatory alongside password strength rules.

## II. Structure & Process

```mermaid
sequenceDiagram
    participant Security as "Security/IAM Team"
    participant Committee as "ISMS Steering Committee"
    participant IT as "IT Operations"
    participant User as "End User"

    Security->>Committee: "Propose password standard, review benchmarks"
    Committee->>Security: "Approve policy and set annual review"
    Security->>IT: "Configure directory/IAM enforcement rules"
    IT->>User: "Apply technical controls at login"
    Security->>Committee: "Report compliance metrics and exceptions"
```

| Field | Description |
|---|---|
| Minimum Length & Complexity | Character-length floor and composition rules, or passphrase guidance where complexity rules are relaxed. |
| Rotation Requirements | Whether and how often passwords must change, distinguishing standard and privileged accounts. |
| Reuse Restrictions | Number of prior passwords that cannot be reused. |
| MFA Requirements | Systems and roles where multi-factor authentication is mandatory. |
| Lockout Thresholds | Failed-attempt count that triggers account lockout, and unlock procedure. |
| Storage & Transmission | Requirement that passwords be hashed at rest and never transmitted in plaintext. |
| Privileged Account Rules | Stricter requirements for admin, service, and root-level accounts, often paired with a password vault. |
| Exception Process | How a system that cannot meet the standard (legacy application) is documented and compensated for. |

Security drafts the standard against current industry guidance, the ISMS steering committee approves it, and IT operations implements enforcement through directory policy and MFA configuration. The policy is reviewed annually and whenever authentication guidance from standards bodies materially changes.

## III. Expected Benefits & Implications

The strongest practical shift in password policy over the last several years is moving away from forced frequent rotation toward passphrase length plus mandatory MFA — rotation policies that force frequent changes reliably push users toward predictable, incrementally modified passwords, which is worse for security than a longer password changed rarely.

| Benefit | Where It Shows Up |
|---|---|
| Fewer credential-based initial-access incidents | Reduced phishing and credential-reuse breach exposure |
| Faster breach investigation | Documented baseline instead of per-system ad hoc rules |
| Regulatory and audit defensibility | A written, enforced standard auditors can test against |
| Reduced helpdesk load from forced resets | Passphrase guidance reduces lockouts compared to complex rotation rules |

Treat MFA coverage, not password complexity, as the metric that actually predicts breach resistance — a compromised password behind MFA is a non-event, while a "strong" password without MFA is still one phishing email away from full account takeover.

Related: [Acceptable Use of Assets Policy](../acceptable-use-of-assets-policy/), [Information Transfer Policy](../information-transfer-policy/).

---
weight: 310
title: "Cloud Access Control Matrix"
description: "A structured record mapping human and service identities to cloud accounts, roles, and permission scopes to enforce least privilege."
icon: "admin_panel_settings"
date: "2026-08-18"
lastmod: "2026-08-18"
draft: false
---

## I. Overview

```mermaid
%%{init: { 'theme': 'base', 'themeVariables': { 'edgeLabelBackground': '#fff' }}}%%
flowchart LR
    A["Manually tracked, drifting\ncloud accounts"] -- "Need for continuous\nposture visibility" --> B["Formal Cloud Access\nControl Matrix"]
    style A fill:#f9f9f9,stroke:#333,stroke-width:3px
    style B fill:#e1f5fe,stroke:#01579b,stroke-width:3px
```

**Definition**: A Cloud Access Control Matrix is a structured inventory of every identity — human user, group, or service account — with access to a cloud account, subscription, or project, together with the role, permission scope, and resource boundary each identity holds.

**Features**:  
( **Ownership** ) Maintained by the cloud security or platform engineering team in coordination with resource owners.  
( **Multi-Cloud Scope** ) Extends the traditional access matrix concept into environments where identities span multiple providers, cross-account roles, and machine-to-machine service accounts.  
( **Least Privilege Verification** ) Confirms whether privileged cloud access matches job function.  
( **Stale Grant Detection** ) Surfaces stale grants and orphaned service accounts that would otherwise remain active.

## II. Structure & Process

| Field | Description |
|---|---|
| Cloud Account/Subscription | The specific account, project, or subscription the entry applies to. |
| Identity Type | Human user, group, federated identity, or service/machine account. |
| Role/Policy Name | The IAM role or managed policy assigned. |
| Permission Scope | Actions permitted, e.g. read-only, contributor, administrator. |
| Resource Scope | Boundary of the grant, e.g. specific resource group, tag, or account-wide. |
| MFA Enforced | Whether multi-factor authentication is required for this identity. |
| Business Justification | Why this identity requires this level of cloud access. |
| Approver | Resource owner or cloud security lead who authorized the grant. |
| Last Review Date | Date of the most recent access recertification. |

```mermaid
sequenceDiagram
    participant Requester as "Requesting Team"
    participant Owner as "Resource/Account Owner"
    participant CloudSec as "Cloud Security/IAM Team"
    participant Auditor as "Internal Audit"

    Requester->>Owner: "Request cloud role or service account access"
    Owner->>CloudSec: "Approve and specify permission scope"
    CloudSec->>CloudSec: "Provision access via IaC and update matrix"
    CloudSec->>Owner: "Send matrix for periodic recertification"
    Owner->>Auditor: "Provide matrix as posture review evidence"
```

The matrix is updated whenever a role, policy, or service account is provisioned or changed, and undergoes full recertification on a fixed cadence — typically monthly for administrative and cross-account roles, and quarterly for standard access — with resource owners attesting each entry is still required.

## III. Best Practices & Comparison

| Document | Primary Purpose | Update Cadence | Owner |
|---|---|---|---|
| Cloud Access Control Matrix | Track which identities can act on which cloud resources | Continuous, with periodic recertification | Cloud security/IAM team, resource owners |
| Cloud Asset Inventory Tracker | Track which resources exist and who owns them | Continuous, discovery-driven | Cloud platform team |
| Cloud Security Configuration Baseline | Define the hardened settings resources must meet | Version-controlled, updated per provider changes | Cloud security architecture team |

- Grant access through roles or groups defined as code, not one-off console changes.
- Require MFA and just-in-time elevation for any administrative or cross-account role.
- Recertify service accounts and machine identities as rigorously as human accounts — they rarely expire on their own.
- Tie every grant to a documented business justification and a named approver.
- Cross-reference entries against the [Cloud Asset Inventory Tracker](../cloud-asset-inventory-tracker/) so access scope never outlives the resource it was granted for.

Related: [Cloud Asset Inventory Tracker](../cloud-asset-inventory-tracker/), [Cloud Security Configuration Baseline](../cloud-security-configuration-baseline/).

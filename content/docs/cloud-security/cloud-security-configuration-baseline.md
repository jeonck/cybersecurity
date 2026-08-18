---
weight: 350
title: "Cloud Security Configuration Baseline"
description: "The approved, enforceable hardening standard cloud resources must meet, derived from recognized benchmarks and checked continuously."
icon: "tune"
date: "2026-08-18"
lastmod: "2026-08-18"
draft: false
---

## I. Overview

```mermaid
%%{init: { 'theme': 'base', 'themeVariables': { 'edgeLabelBackground': '#fff' }}}%%
flowchart LR
    A["Inconsistent, per-team\ncloud configurations"] -- "Need for a single\nenforceable hardening standard" --> B["Formal Cloud Security\nConfiguration Baseline"]
    style A fill:#f9f9f9,stroke:#333,stroke-width:3px
    style B fill:#e1f5fe,stroke:#01579b,stroke-width:3px
```

**Definition**: A Cloud Security Configuration Baseline defines the approved secure settings — IAM policy limits, storage access defaults, network exposure rules, logging requirements — that every cloud resource of a given type must meet, expressed as controls a CSPM tool or policy engine can check automatically.

**Features**:  
( **Ownership** ) Owned by the cloud security architecture team and implemented jointly with platform engineering through infrastructure-as-code and policy-as-code.  
( **Drift Prevention** ) Counters how cloud configuration drifts fast when resources are cheap to create and self-service by design.  
( **Enforced Standard** ) Turns "secure by default" from an aspiration into an enforced, auditable standard.  
( **Recognized Derivation** ) Typically derived from recognized references such as CIS Benchmarks or provider well-architected frameworks.

## II. Structure & Process

| Field | Description |
|---|---|
| Service/Resource Type | The cloud service the control applies to, e.g. object storage, IAM, VPC. |
| Control ID | Unique identifier cross-referenced to the standard it derives from. |
| Setting/Requirement | The specific configuration required, e.g. public access blocked by default. |
| Standard Reference | Source standard, such as a CIS Benchmark or NIST control. |
| Enforcement Mechanism | How it is enforced, e.g. service control policy, policy-as-code, CSPM rule. |
| Compliance Status | Current scan result across the resource population. |
| Exception Process | How and for how long a documented deviation may be approved. |
| Last Reviewed | Date the control was last validated against provider changes. |

```mermaid
sequenceDiagram
    participant Arch as "Cloud Security Architecture"
    participant Platform as "Platform Engineering"
    participant CSPM as "CSPM Tooling"
    participant Owner as "Resource Owner"

    Arch->>Arch: "Define baseline from CIS Benchmarks/standards"
    Arch->>Platform: "Publish baseline as policy-as-code"
    Platform->>Platform: "Implement via IaC and guardrails"
    CSPM->>CSPM: "Continuously scan resources against baseline"
    CSPM->>Owner: "Flag non-compliant resource"
    Owner->>Arch: "Remediate or request time-boxed exception"
```

The baseline is version-controlled and reviewed whenever a provider introduces new services or changes default behavior, while individual resources are checked continuously by CSPM tooling rather than on a periodic audit cycle — exceptions are logged with an expiry date and revisited at each baseline review.

## III. Best Practices & Comparison

| Document | Primary Purpose | Update Cadence | Owner |
|---|---|---|---|
| Cloud Security Configuration Baseline | Define the hardened settings all cloud resources must meet | Version-controlled, updated per provider changes | Cloud security architecture team |
| Cloud Access Control Matrix | Track which identities can act on which resources | Continuous, with periodic recertification | Cloud security/IAM team |
| Cloud Asset Inventory Tracker | Track which resources exist to be checked against the baseline | Continuous, discovery-driven | Cloud platform team |

- Derive the baseline from a recognized standard, such as CIS Benchmarks, rather than writing controls from scratch.
- Enforce through policy-as-code and service control policies, not documentation teams are expected to remember.
- Treat every exception as time-boxed and tracked, never a silent permanent deviation.
- Version the baseline alongside provider service updates so new resource types are never left unscoped.
- Validate continuously with CSPM scanning instead of relying on periodic manual configuration review.

Related: [Cloud Access Control Matrix](../cloud-access-control-matrix/), [Cloud Asset Inventory Tracker](../cloud-asset-inventory-tracker/).

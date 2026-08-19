---
weight: 9050
title: "Identity Provider (IdP)"
description: "The trusted authority that authenticates users and issues the assertions or tokens that relying service providers use to grant access."
icon: "admin_panel_settings"
date: "2026-08-18"
lastmod: "2026-08-18"
draft: false
---

## I. Overview

```mermaid
%%{init: { 'theme': 'base', 'themeVariables': { 'edgeLabelBackground': '#fff' }}}%%
flowchart LR
    A["Each service manages\nuser identity separately"] -- "Centralized identity management and\nunified security policy" --> B["Unified identity management\ncentered on the IdP"]
    style A fill:#f9f9f9,stroke:#333,stroke-width:3px
    style B fill:#e1f5fe,stroke:#01579b,stroke-width:3px
```

**Definition**: A trusted authority that manages user authentication information and, once a user is successfully authenticated, issues a security token (an assertion or token) that a relying service provider (**SP**) can trust.

**Features**:  
( **Central Authentication** ) A user authenticates once at the **IdP** and can then access every connected **SP** — the core mechanism behind **SSO**  
( **Identity Information Delivery** ) Securely passes a user's identity information (name, email, etc.) to the **SP** for account creation and login  
( **Standards Compliance** ) Uses standard protocols such as **SAML** and **OpenID Connect** to guarantee secure, interoperable communication with the **SP**  
( **SSO Ecosystem** ) Unifies authentication across multiple services, improving the user experience and the efficiency of security management  

## II. Mechanism & Components

### A. Federated Identity Authentication Flow

```mermaid
sequenceDiagram
    participant U as User
    participant IdP as Identity Provider (IdP)
    participant SP1 as Service Provider 1 (SP1)
    participant SP2 as Service Provider 2 (SP2)

    U->>SP1: Attempt to access service
    SP1->>IdP: Authentication request (SAML/OIDC)
    IdP->>U: Request authentication (ID/PW, MFA)
    U->>IdP: Provide authentication information
    IdP-->>U: Authentication succeeds (assertion / token issued)
    U-->>SP1: Deliver assertion / token
    SP1->>SP1: Verify assertion / token, create session
    SP1-->>U: Grant service access

    Note over U,SP2: Accessing another service (SP2) reuses the IdP session
    U->>SP2: Attempt to access service
    SP2->>IdP: Authentication request (SAML/OIDC)
    Note over IdP: Confirms an already-authenticated user session exists
    IdP-->>U: Immediately issue assertion / token
    U-->>SP2: Deliver assertion / token
    SP2->>SP2: Verify assertion / token, create session
    SP2-->>U: Grant service access
```

### B. Major SSO Protocols and the IdP's Role

| Protocol | IdP's Role | SP's Role |
|:---:|----------|----------|
| **SAML** | Generates and issues the **SAML Assertion** | Receives and verifies the **SAML Assertion** |
| **OpenID Connect** | Issues the **ID Token** and **Access Token** | Receives and verifies the **ID Token** / **Access Token** |
| **OAuth 2.0** | Issues the **Access Token** (acts as the authorization server) | Receives the **Access Token** and checks resource-access privileges |

## III. Expected Benefits & Implications

Centralizing authentication behind an IdP pays off most clearly at the moments organizations tend to underestimate: onboarding and offboarding. Provisioning a new hire's access to every connected **SP** becomes a single account creation instead of N separate signups, and revoking a departing employee's access becomes a single account disable instead of a checklist that's easy to leave incomplete.

| Benefit | Where It Shows Up |
|---|---|
| Faster onboarding/offboarding | Time-to-provision and time-to-deprovision across every connected SP |
| Consistent security policy | One place to enforce MFA, password rules, and session timeouts |
| Reduced credential sprawl | Fewer help-desk password resets, fewer reused passwords across services |

The implication organizations tend to miss is that centralizing authentication also centralizes risk — an IdP is worth adopting specifically because it concentrates control, but that same concentration means IdP security investment (MFA, monitoring, admin console access) should scale ahead of the number of services it connects, not after.

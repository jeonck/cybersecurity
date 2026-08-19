---
weight: 9130
title: "Single Sign-On (SSO)"
description: "An authentication approach that lets a user log in once with one identity to reach multiple applications and services."
icon: "login"
date: "2026-08-18"
lastmod: "2026-08-18"
draft: false
---

## I. Overview

```mermaid
%%{init: { 'theme': 'base', 'themeVariables': { 'edgeLabelBackground': '#fff' }}}%%
flowchart LR
    A["Multiple applications\n(App1, App2, App3...)"] -- "Single authentication (1st login)" --> B["SSO service\n(Identity Provider)"]
    B -- "Issues authentication ticket" --> A
    style A fill:#f9f9f9,stroke:#333,stroke-width:3px
    style B fill:#e1f5fe,stroke:#01579b,stroke-width:3px
```

**Definition**: An authentication method that lets a user log into multiple applications and services using a single **ID** and password.

**Features**:  
( **Greater User Convenience** ) Eliminates repeated login steps, significantly improving the user experience and boosting productivity  
( **Stronger Security** ) Reduces the burden of managing complex passwords and makes it easier to apply strong, centralized authentication such as **MFA**  
( **Management Efficiency** ) Centralizes account creation, deletion, and privilege management, reducing the overall IT administration burden  
( **Improved Accessibility** ) Delivers a consistent user experience across mobile devices and other device environments  

## II. Mechanism & Components

### A. SSO Authentication Flow (Federated Identity)

```mermaid
sequenceDiagram
    participant User as User
    participant SP as Service Provider
    participant IdP as Identity Provider

    User->>SP: Attempt to access service
    SP->>User: Redirect to IdP (authentication request)
    User->>IdP: Enter ID/PW + MFA, etc.
    IdP-->>User: Authentication succeeds (SAML assertion / ID token issued)
    User->>SP: Deliver assertion/token received from IdP
    SP->>SP: Verify assertion/token, create session
    SP-->>User: Grant service access
```

### B. Major Protocols Used to Implement SSO

| Protocol | Key Characteristics | How It Works |
|:---:|----------|----------|
| **SAML (Security Assertion Markup Language)** | An **XML**-based standard, mainly used for web-based service integration | User accesses **SP** → redirected to **IdP** → **IdP** authenticates and issues a **SAML Assertion** → **SP** verifies the assertion and grants access |
| **OAuth 2.0** | An authorization protocol used to delegate resource-access privileges | User delegates access to **SP**'s resources to the **IdP** → **IdP** issues an **Access Token** → **SP** verifies the token and grants resource access |
| **OpenID Connect (OIDC)** | An identity layer built on **OAuth 2.0** that supplies user authentication information (ID Token) | Adds an **ID Token** (user info) on top of the **OAuth 2.0** flow → **SP** verifies the ID Token and identifies the user |

## III. Expected Benefits & Implications

SSO's biggest measurable win usually isn't user convenience — it's the ability to instantly revoke access to every connected application from one place when someone leaves, instead of chasing down accounts app by app. Track offboarding completion time as the KPI, not login friction, when justifying an SSO investment to leadership.

| Benefit | Where It Shows Up |
|---|---|
| Faster offboarding | Time-to-full-deprovisioning across every connected SP |
| Fewer help-desk password resets | Support ticket volume |
| Consistent MFA enforcement | Fewer weak-auth paths left unmonitored across services |

The flip side of that concentration is worth stating plainly: SSO doesn't reduce risk so much as relocate it entirely onto the IdP, so the security budget saved on per-app password policies should be reinvested directly into IdP hardening — MFA, session management, monitoring — rather than treated as a net security win on its own.

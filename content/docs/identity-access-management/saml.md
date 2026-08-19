---
weight: 9120
title: "SAML (Security Assertion Markup Language)"
description: "An XML-based open standard for exchanging authentication data between an identity provider and a service provider, the de facto standard for web-based SSO."
icon: "handshake"
date: "2026-08-18"
lastmod: "2026-08-18"
draft: false
---

## I. Overview

```mermaid
%%{init: { 'theme': 'base', 'themeVariables': { 'edgeLabelBackground': '#fff' }}}%%
flowchart LR
    A["Fragmented authentication\nper individual service"] -- "Standardized SSO and\ncross-domain trust federation" --> B["SAML-based\nidentity federation"]
    style A fill:#f9f9f9,stroke:#333,stroke-width:3px
    style B fill:#e1f5fe,stroke:#01579b,stroke-width:3px
```

**Definition**: An **XML**-based open standard protocol for securely exchanging user authentication information in web-based distributed environments.

**Features**:  
( **XML-Based** ) Represents a user's identity, attributes, and privileges as an **XML**-formatted assertion for exchange  
( **Web SSO Standard** ) **SAML 2.0** has become the de facto standard for implementing **SSO** (Single Sign-On) in browser-based environments  
( **Federated Identity** ) Establishes a trust relationship between an **IdP** and an **SP** in different security domains, enabling them to share user authentication information  
( **Industry Standard** ) Standardized under the leadership of **OASIS** (Organization for the Advancement of Structured Information Standards)  

## II. Mechanism & Components

### A. SAML 2.0-Based SSO Flow (SP-Initiated)

```mermaid
sequenceDiagram
    participant User as User
    participant SP as Service Provider (SP)
    participant IdP as Identity Provider (IdP)

    User->>SP: Attempt to access service
    SP->>IdP: Send SAML AuthnRequest
    IdP->>User: Request authentication (ID/PW, MFA)
    User->>IdP: Provide authentication information
    IdP-->>User: Authentication succeeds (SAML assertion issued)
    User-->>SP: SAML Response (includes assertion)
    SP->>SP: Verify assertion, create session
    SP-->>User: Grant service access
```

### B. SAML Message Components

| Component | Description | Security Value |
|----------|----------|----------|
| **SAML Assertion** | An **XML** document carrying the user's identity, attributes, and authentication/authorization information | The core artifact exchanged for user authentication |
| **SAML Authority** | The **IdP** (identity authority) or the **SP** (service provider) | Performs the authentication or authorization role |
| **SAML Binding** | The transport mechanism for **SAML** messages, e.g. **HTTP POST**, **HTTP Redirect** | Defines the message-delivery channel |
| **SAML Metadata** | Meta information exchanged to establish trust between **IdP** and **SP** | Supports interoperability and secure configuration |

## III. Comparison & Application

| Protocol | Best Fit | Weakness |
|---|---|---|
| SAML 2.0 | Enterprise SSO, legacy and government IdPs | XML complexity, heavier payload, no native mobile support |
| OAuth 2.0 + OIDC | API access, mobile apps, SPAs | Requires careful scope/claims design; not always present in older enterprise IdPs |

Default to OIDC for anything greenfield — SAML earns its place only when the identity provider on the other side of the integration (many enterprise IdPs, government and education systems) doesn't speak OIDC yet. Treat SAML support as a compatibility requirement to satisfy existing IdP relationships, not as a design goal for new systems, since new protocol investment in the identity space has effectively moved to the OAuth/OIDC family.

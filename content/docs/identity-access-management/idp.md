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

## III. Advanced Topics & Comparison

### A. Why IdP Security Matters, and Potential Threats

- **Single Point of Failure**: If the **IdP** goes down, every connected service becomes unusable
- **Centralized Attack Target**: Compromising the **IdP** account can grant access to every connected service (credential stuffing, phishing, etc.)
- **Token/Assertion Vulnerabilities**: Flawed verification logic or reuse of a stolen token can lead to session hijacking

### B. IdP Security Hardening Best Practices

- **Strong Authentication Mechanisms**: Apply **MFA** (Multi-Factor Authentication), password policies, and **SSO** session timeouts
- **Protocol Security**: Require **HTTPS**, thoroughly verify the signature and encryption of SAML/OIDC assertions and tokens
- **Access Control and Logging**: Minimize access to the **IdP** admin console; keep detailed audit logs and monitoring
- **Regular Vulnerability Reviews**: Apply the latest security patches to the **IdP** solution and conduct periodic security audits

> **Key Point**: Because the **IdP** is an organization's identity management hub, maintaining strong security for the **IdP** itself and safely configuring every connected **SP** are both essential to overall security.

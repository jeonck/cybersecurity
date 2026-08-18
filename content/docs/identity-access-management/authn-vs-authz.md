---
weight: 9030
title: "Authentication vs. Authorization"
description: "Why verifying who a user is (authentication) and deciding what they can do (authorization) are distinct, sequential steps in access control."
icon: "compare_arrows"
date: "2026-08-18"
lastmod: "2026-08-18"
draft: false
---

## I. Overview

```mermaid
%%{init: { 'theme': 'base', 'themeVariables': { 'edgeLabelBackground': '#fff' }}}%%
flowchart LR
    A["A single\nuser request"] -- "Identity verification, then privilege granting" --> B["Trust-based\naccess control"]
    style A fill:#f9f9f9,stroke:#333,stroke-width:3px
    style B fill:#e1f5fe,stroke:#01579b,stroke-width:3px
```

**Definition**: Authentication verifies who a subject claims to be, while authorization determines what an authenticated subject is permitted to do — two distinct but sequential steps in access control.

**Features**:  
( **Identity Verification (Authentication)** ) Confirms whether a subject's claimed identity is genuine, establishing trust at the system's entry point  
( **Privilege Control (Authorization)** ) Defines the scope of an authenticated user's actions and grants resource access under the principle of least privilege  
( **Security Visibility** ) Authentication and authorization logs trace a subject's activity and provide accountability when incidents occur  

## II. Mechanism & Components

### A. Relationship Between Authentication and Authorization

```mermaid
sequenceDiagram
    participant User as Subject
    participant AuthN as Authentication Server (AuthN)
    participant AuthZ as Authorization Server (AuthZ)
    participant Resource as Resource (Object)

    User->>AuthN: Submit proof of identity (ID / PW / MFA)
    AuthN-->>User: Authentication succeeds, token issued (JWT / Session)
    User->>AuthZ: Request resource access with token
    AuthZ->>AuthZ: Verify privileges (ACL / RBAC)
    AuthZ-->>Resource: Grant access
    Resource-->>User: Provide resource
```

> **Explanation**: When a subject makes an access request, its identity is first verified through authentication; the resulting token or session is then used by the authorization server to decide whether access is permitted.

### B. Key Comparison Points

| Comparison Item | Authentication | Authorization |
|----------|----------------------|-------------------|
| **Core Question** | "Who are you?" | "What are you allowed to do?" |
| **Sequencing** | A prerequisite for authorization (performed first) | Performed after authentication completes |
| **Implementing Technologies** | ID/PW, MFA, FIDO, biometric authentication | ACL, RBAC, OAuth 2.0, IAM policies |
| **What Is Presented** | Credentials | Proof of authorization (access token, scope) |
| **Result on Failure** | 401 Unauthorized (identity not confirmed) | 403 Forbidden (insufficient privileges) |

## III. Advanced Topics & Comparison

### A. Evolution of Authentication: Passkeys and MFA

- **MFA (Multi-Factor Authentication)**: Combines two or more of knowledge (password), possession (OTP), and inherence (biometrics)
- **FIDO2 / Passkey**: Implements a passwordless environment, cutting off phishing attacks at the source

### B. Evolution of Authorization: OAuth 2.0 and ABAC

- **OAuth 2.0**: Delegates only resource-access privileges to third-party applications without exposing the user's password
- **ABAC (Attribute-Based)**: Dynamic authorization based on attributes beyond just job title — including access time, location, and device security posture

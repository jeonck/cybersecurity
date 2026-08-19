---
weight: 9100
title: "OpenID Connect (OIDC)"
description: "An identity layer built on top of OAuth 2.0 that adds standardized user authentication via a signed ID Token."
icon: "badge"
date: "2026-08-18"
lastmod: "2026-08-18"
draft: false
---

## I. Overview

```mermaid
%%{init: { 'theme': 'base', 'themeVariables': { 'edgeLabelBackground': '#fff' }}}%%
flowchart LR
    A["Incomplete authentication with\nOAuth 2.0 alone (authorization only)"] -- "A standardized identity layer with\nthe ID Token (JWT)" --> B["Standard, unified\nauthentication via OIDC"]
    style A fill:#f9f9f9,stroke:#333,stroke-width:3px
    style B fill:#e1f5fe,stroke:#01579b,stroke-width:3px
```

**Definition**: An **OpenID**-based authentication protocol, built on top of **OAuth 2.0**, for securely sharing a user's authentication information with a mutually trusted service (**SP**).

**Features**:  
( **Simplified SSO** ) Gives users a unified login experience across multiple services while easing the account-management burden on IT administrators  
( **Standardized Identity Information** ) Delivers consistent user profile information (name, email, profile photo, etc.) through a **JWT**-based **ID Token**  
( **Compatibility** ) Being built on **OAuth 2.0**, it can be applied easily across web, mobile, desktop, and other client environments  
( **Authentication Plus Authorization** ) **OAuth 2.0** focuses on granting authorization; OIDC adds authentication on top, supporting user identification and SSO  

## II. Mechanism & Components

### A. OIDC Authentication Flow (Authorization Code Flow)

```mermaid
sequenceDiagram
    participant User as User
    participant Client as Client App
    participant IdP as OIDC Provider (IdP)
    participant RS as Resource Server

    User->>Client: Request to use service
    Client->>IdP: Authorization request (code, client_id, redirect_uri)
    IdP->>User: Request login (ID/PW, MFA)
    User->>IdP: Submit authentication information
    IdP-->>User: Authentication succeeds (authorization code issued)
    User-->>Client: Deliver authorization code
    Client->>IdP: Present authorization code (request access token, ID token)
    IdP-->>Client: Issue access token, ID token
    Client->>RS: Present access token
    RS-->>Client: Grant resource access
```

### B. Key Components of OIDC

| Component | Description | Role |
|:---:|----------|----------|
| **End-User** | The end user trying to use the service | Provides identity information and consents to access |
| **Client** | The application requesting resource access on the user's behalf | Obtains and uses the **Authorization Code** / **ID Token** / **Access Token** |
| **Authorization Server (IdP)** | Authenticates the user and issues the **Access Token** and **ID Token** | Handles **End-User** authentication and authorization |
| **Resource Server** | The server hosting the protected resource (API) | Verifies the **Access Token** and provides the resource to the client |
| **ID Token** | A **JWT** (JSON Web Token) carrying the user's authentication information | Confirms the user's identity and supplies basic profile information |

## III. Vulnerabilities & Security Measures

| Attack Vector | Primary Control |
|---|---|
| ID Token / access token theft | Enforce HTTPS on every channel; short token lifetimes |
| Redirect URI manipulation | Allowlist only registered Redirect URIs at the IdP |
| CSRF via forged authentication requests | Unique `state` parameter per request, verified on callback |
| Stolen authorization code replay | PKCE, especially for public/mobile clients |
| Forged or unverified ID Token | Verify signature, `exp`, `iss`, and `aud` on every ID Token — never trust an unverified claim |

The ID Token is where most OIDC integration bugs actually live, because it's trivial to decode the JWT and read its claims without ever validating the signature, issuer, or audience — a token that decodes cleanly is not the same as a token that has been verified. Treat "did we call the JWT verification library, not just the JWT parsing library" as a mandatory review question for any OIDC client integration, since the two are easy to confuse and only one of them is actually secure.

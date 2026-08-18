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

## III. Advanced Topics & Comparison

### A. OIDC Security Vulnerabilities

- **ID Token/Access Token theft**: Risk of account takeover if a token leaks due to a client vulnerability or a lack of **HTTPS**
- **Weak Redirect URI validation**: Processing a callback outside the registered **Redirect URI** exposes the flow to attack
- **No state parameter**: Vulnerable to CSRF attacks that can trigger malicious redirects
- **IdP-level vulnerabilities**: If the **IdP**'s own security is weak, every connected service becomes vulnerable

### B. OIDC Security Hardening

- **Enforce HTTPS**: Use **HTTPS** on every communication channel to encrypt data in transit
- **Redirect URI allowlisting**: Allow only the **Redirect URI**s registered with the **IdP**, preventing callback-address tampering
- **Use the state parameter**: Generate a unique **state** value on each authentication request and verify it on callback to defend against CSRF
- **PKCE (Proof Key for Code Exchange)**: Prevents token issuance after a stolen code — especially important for public clients and mobile apps
- **ID Token verification**: Verify the **JWT** signature, expiration (**exp**), issuer (**iss**), audience (**aud**), and other required claims

> **Key Point**: Because OIDC extends **OAuth 2.0** to add user authentication, the secure issuance, transmission, and verification of the **ID Token**, together with strong **IdP** security, are essential.

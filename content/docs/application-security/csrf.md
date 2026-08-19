---
weight: 4080
title: "CSRF (Cross-Site Request Forgery)"
description: "A web attack technique that hijacks a user's authenticated session to make a target site perform actions the user never intended."
icon: "swap_horiz"
date: "2026-08-18"
lastmod: "2026-08-18"
draft: false
---

## I. Overview

```mermaid
%%{init: { 'theme': 'base', 'themeVariables': { 'edgeLabelBackground': '#fff' }}}%%
flowchart LR
    A["Authenticated user session"] -- "Forged Request" --> B["Unintended action\non the server"]
    style A fill:#f9f9f9,stroke:#333,stroke-width:3px
    style B fill:#e1f5fe,stroke:#01579b,stroke-width:3px
```

**Definition**: CSRF (Cross-Site Request Forgery) is an attack technique that makes a user's browser send a request an attacker has designed — to modify, delete, or register data — to a specific website, without the user's knowledge or intent.

**Features**:  
( **Reliance on Session Trust** ) The user must already be logged in to the target site so that a valid session cookie exists in the browser.  
( **Requires User Interaction** ) The victim must click an attacker-crafted malicious link or visit a page where a script executes.  
( **Predictable Parameters** ) The attacker must be able to know the target server's request parameter structure in advance in order to forge it.

## II. Mechanism & Components

### A. CSRF Attack Scenario Process

```mermaid
sequenceDiagram
    participant V as "Victim"
    participant A as "Attacker Server"
    participant S as "Target Web Server (Bank)"

    Note over V,S: "0. Victim is already logged in to the target site (S)"
    V->>A: "Visits malicious page (clicks attacker's email/post link)"
    A-->>V: "Responds with CSRF script (e.g. auto-submitting form)"
    Note over V: "Browser sends the forged request"
    V->>S: "GET/POST /transfer?to=hacker&amount=1000"
    Note right of S: "S trusts it as a legitimate request because it sees the victim's cookie"
    S-->>V: "Request processed (unintended transfer occurs)"
```

### B. Key Comparison: CSRF vs. XSS

| Comparison | XSS (Cross-Site Scripting) | CSRF (Cross-Site Request Forgery) |
|:---:|---------------------------|----------------------------------|
| **Target** | Client (user's browser) | Server (web application service) |
| **Attack Principle** | Execution of a malicious script | Hijacking of the user's privileges (sending a forged request) |
| **Core Goal** | Information theft (cookies, sessions, etc.) | State change (modifying, deleting data, transferring funds, etc.) |
| **Point of Action** | Data processing inside the user's browser | Business logic executed on the server side |

## III. Vulnerabilities & Security Measures

| Control | Mechanism | Security Effect |
|----------|----------|----------|
| CSRF Token | Server-issued one-time token validated on every write request | Detects forged requests that lack a valid token |
| SameSite Cookie | `Lax` or `Strict` attribute on session cookies | Blocks automatic cookie transmission from third-party sites |
| Double Submit Cookie | Compares cookie value against a request-parameter token | Works even where server-side session storage is limited |
| Re-authentication | Requires password or OTP before sensitive actions | Blocks final execution even if a forged request reaches the server |

No single control here is sufficient on its own — SameSite cookies stop most forged cross-origin requests today, but they depend on browser compliance the application doesn't control, which is exactly why a CSRF token check on the server side has to stay in place as the actual authoritative defense. Treat SameSite as defense-in-depth, not a replacement for token validation.

---
weight: 4100
title: "XSS (Cross-Site Scripting)"
description: "A client-side web vulnerability where an attacker injects a malicious script that executes in the browser of a user who views the page."
icon: "code"
date: "2026-08-18"
lastmod: "2026-08-18"
draft: false
---

## I. Overview

```mermaid
%%{init: { 'theme': 'base', 'themeVariables': { 'edgeLabelBackground': '#fff' }}}%%
flowchart LR
    A["Malicious script injection"] -- "Execution in the browser and\nsession hijacking" --> B["Abuse of user privileges\n(Session Hijacking)"]
    style A fill:#f9f9f9,stroke:#333,stroke-width:3px
    style B fill:#e1f5fe,stroke:#01579b,stroke-width:3px
```

**Definition**: XSS (Cross-Site Scripting) is a security vulnerability in which an attacker injects a malicious script into a web application so that the script executes in the browser of any user who views the page.

**Features**:  
( **Session Hijacking** ) Steals the session token stored in the user's cookie to take over the account and perform actions on the victim's behalf.  
( **Personal Information Leakage** ) Uses the script to send sensitive information from the page to an external server or redirect the user to a phishing site.  
( **User Deception** ) Serves as a foothold for arbitrarily modifying web page content or distributing malicious software.

## II. Mechanism & Components

### A. Stored XSS Process

```mermaid
sequenceDiagram
    participant H as "Attacker (Hacker)"
    participant S as "Web Server (DB)"
    participant V as "Victim"

    H->>S: "Saves a post containing a malicious script"
    V->>S: "Requests to view the post"
    S-->>V: "Responds with HTML containing the malicious script"
    Note over V: "Browser automatically executes the script"
    V->>H: "Sends session cookie"
```

### B. Detailed Comparison of Attack Types

| Type | Attack Method | Script Storage Location | Primary Attack Surface |
|:---:|----------|:---------------:|--------------|
| **Stored XSS** | Permanently stores the script in a bulletin board, profile, etc. | Server database ( **DB** ) | Bulletin boards, comments, guestbooks |
| **Reflected XSS** | Input such as a search term is immediately reflected back into the response page | Response message ( **Non-persistent** ) | Search results, error messages, **URL** parameters |
| **DOM-based XSS** | A client-side script dynamically processes **DOM** data | Client browser ( **DOM** ) | `innerHTML`, `document.write` in **JavaScript** |

## III. Advanced Topics & Comparison

### A. Technical Countermeasures (Secure Coding)

- **Output Encoding**: When rendering user input as **HTML**, convert special characters ( `<`, `>`, `&`, `"`, etc. ) into **HTML Entities** to prevent execution.
- **Input Filtering**: Apply whitelist-based validation against dangerous tags and event handlers such as `<script>`, `onerror`, and `onload`.
- **Security Headers**:  
  - **Content Security Policy** ( **CSP** ): Enforces a browser policy that only allows scripts from approved domains to execute.  
  - **X-XSS-Protection**: Enables the browser's built-in **XSS** filter to help block attacks.

### B. Browser-Side Security Measures

| Measure | Details | Security Effect |
|----------|----------|----------|
| **HttpOnly Cookie** | Blocks **JavaScript** access via `document.cookie` | Fundamentally prevents session cookie theft ( **Session Hijacking** ) through **XSS** |
| **Secure Cookie** | Transmits cookies only over the **HTTPS** protocol | Defends against cookie sniffing on the network segment |
| **SameSite Cookie** | Controls how cookies are sent to third-party sites ( **Lax** / **Strict** ) | Defends against **CSRF** attacks and mitigates some **XSS** damage |

> **Key Point**: The foundation of **XSS** defense is assuming that "all user input is untrusted," and applying thorough **entity encoding** at the output stage together with a **CSP**.

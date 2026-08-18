---
weight: 420
title: "Secure Coding Checklist"
description: "A per-release checklist of secure coding requirements covering input validation, authentication, and safe handling of common vulnerability classes."
icon: "checklist"
date: "2026-08-18"
lastmod: "2026-08-18"
draft: false
---

## I. Overview

```mermaid
%%{init: { 'theme': 'base', 'themeVariables': { 'edgeLabelBackground': '#fff' }}}%%
flowchart LR
    A["Vulnerabilities found only\nlate, in production"] -- "Need to shift security\nleft in the SDLC" --> B["Formal Secure\nCoding Checklist"]
    style A fill:#f9f9f9,stroke:#333,stroke-width:3px
    style B fill:#e1f5fe,stroke:#01579b,stroke-width:3px
```

**Definition**: A Secure Coding Checklist is the standardized set of requirements developers verify before code is merged or released — covering input validation, output encoding, authentication and session handling, and safe use of database and file-system APIs.

**Features**:  
( **Ownership** ) Maintained by the AppSec team and applied by engineering during development and code review.  
( **Why Needed** ) Vulnerability classes like **SQL injection**, **XSS** (Cross-Site Scripting), and **CSRF** (Cross-Site Request Forgery) are well understood and well documented, yet still ship into production when developers have no standard to check against.  
( **Concrete Gate** ) Turns "know the OWASP Top 10" into a concrete, auditable per-release gate.

## II. Structure & Process

```mermaid
sequenceDiagram
    participant Dev as "Developer"
    participant Reviewer as "Peer Reviewer"
    participant SAST as "SAST Tool"
    participant AppSec as "AppSec Team"

    Dev->>Dev: "Implement feature against checklist requirements"
    Dev->>SAST: "Run static analysis on commit"
    SAST-->>Dev: "Flag checklist violations"
    Dev->>Reviewer: "Submit pull request with checklist attached"
    Reviewer->>Reviewer: "Verify unresolved items manually"
    Reviewer->>AppSec: "Escalate unresolved high-severity items"
    AppSec->>Dev: "Approve merge or request changes"
```

| Field | Description |
|---|---|
| Category | Weakness class covered, e.g. **Input Validation**, **Authentication**, **Session Management**, **Output Encoding** |
| Requirement | Specific, testable rule (e.g. "use parameterized queries, never string-concatenated SQL") |
| Applies To | Language, framework, or component the rule targets |
| Verification Method | How compliance is confirmed — code review, SAST rule, or manual test |
| Severity if Violated | Impact rating used to decide whether a violation blocks release |
| Reference | Link to the underlying standard, e.g. **OWASP ASVS** (Application Security Verification Standard) control ID |
| Sign-off | Reviewer and date confirming the checklist was completed for the release |

The checklist is applied on every pull request and re-validated at release time; AppSec updates the requirement set quarterly as new weakness classes emerge.

## III. Best Practices & Comparison

| Document | Primary Purpose | Update Cadence | Owner |
|---|---|---|---|
| Secure Coding Checklist | Prevent known weakness classes during development | Per pull request | AppSec + Engineering |
| [Static Code Analysis Log](../static-code-analysis-log/) | Automated detection of violations already in code | Per build / commit | AppSec + Engineering |
| OWASP ASVS | Comprehensive verification standard the checklist is derived from | On standard revision | AppSec |
| [Web Application Vulnerability Tracker](../web-application-vulnerability-tracker/) | Track exploitable findings after code is deployed | Per scan / pentest cycle | AppSec |

- Derive checklist items from OWASP ASVS or an equivalent standard rather than inventing rules ad hoc.
- Require parameterized queries and ORM-safe data access as a non-negotiable rule for all database interaction.
- Mandate output encoding at every point untrusted data reaches HTML, JavaScript, or a URL context to prevent XSS.
- Pair the checklist with automated SAST rules so common violations are caught before human review.
- Revisit the checklist whenever a new vulnerability class is discovered in production, and add a corresponding rule.

Related: [Static Code Analysis Log](../static-code-analysis-log/), [Web Application Vulnerability Tracker](../web-application-vulnerability-tracker/)

---
weight: 5130
title: "Korea's Data 3 Acts"
description: "The legal basis for using pseudonymized and anonymized data in Korea, and the procedure for combining pseudonymized data across data controllers."
icon: "gavel"
date: "2026-08-18"
lastmod: "2026-08-18"
draft: false
---

## I. Overview

```mermaid
%%{init: { 'theme': 'base', 'themeVariables': { 'edgeLabelBackground': '#fff' }}}%%
flowchart LR
    A["Data protection\n(Regulation)"] -- "introducing pseudonymized data\n(safe reuse)" --> B["Data economy\n(Innovation)"]
    style A fill:#f9f9f9,stroke:#333,stroke-width:3px
    style B fill:#e1f5fe,stroke:#01579b,stroke-width:3px
```

**Definition**: The Data 3 Acts are a body of law, created by amending the Personal Information Protection Act, the Act on Promotion of Information and Communications Network Utilization, and the Credit Information Use and Protection Act, that clearly defines the scope of pseudonymizing and using personal information and unifies the surrounding legal framework.

**Background and key value**:  
( **Unifying regulation** ) Consolidates personal-information-related laws that had been scattered across different ministries, preventing confusion in enforcement and improving efficiency.  
( **Enabling data use** ) Establishes a legal basis for using pseudonymized data without the data subject's consent for public-interest purposes such as statistics compilation and scientific research.  
( **Building trust** ) Mandates technical and administrative safeguards, including a ban on re-identification, to balance protecting data subjects' rights with driving industry innovation.

## II. Mechanism & Components

### Data Classification by Identifiability

```mermaid
flowchart LR
    A["Personal information\ndirectly identifies an individual"] -->|"pseudonymization"| B["Pseudonymized data\nnot identifiable without additional information"]
    B -->|"anonymization"| C["Anonymized data\ncompletely and irreversibly anonymous"]

    A --> A1["Data subject consent required\nlimited use"]
    B --> B1["Usable without consent\nstatistics / research / public-interest records"]
    C --> C1["Personal Information Protection Act\ndoes not apply, free use"]
```

| Category | Definition | Scope of Use |
|------|------|--------------|
| Personal information | Information that can directly identify a specific individual | Limited use with the data subject's consent |
| Pseudonymized data | Information processed so that a specific individual cannot be identified without additional information | Statistics compilation, scientific research, public-interest record preservation (usable without consent) |
| Anonymized data | Information from which an individual can no longer be identified, considering time, cost, and technology | Free, unrestricted use (the Personal Information Protection Act does not apply) |

### Technical Protection Measures for Processing Pseudonymized Data

- **Preventing re-identification**: Mandates separate storage of the additional information, access control, and physical/technical safeguards.
- **Prohibited acts**: Re-identifying a specific individual is prohibited (violations carry administrative fines and criminal penalties).

## III. Adoption Considerations & Security Measures

| Risk | Primary Control |
|---|---|
| Re-identifying a pseudonymized individual | Legal prohibition — administrative fines and criminal penalties |
| Uncontrolled combination of pseudonymized data across controllers | Combination permitted only through a specialized data combination institution |
| Treating "pseudonymized" as equivalent to "anonymized" | Additional-information separation, access control, and adequacy review before release |

The single biggest compliance trap in practice is treating pseudonymized data as if it were anonymized — it isn't, and the additional-information separation requirement exists precisely because re-identification is one recombination away for as long as that additional information exists anywhere. Cross-controller combination has to go through a specialized institution's request-combine-review-release process rather than a bespoke bilateral data-sharing arrangement; an ad hoc combination outside that channel is a Data 3 Acts violation regardless of how good the intentions behind it were.

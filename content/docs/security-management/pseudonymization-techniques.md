---
weight: 5160
title: "5 Pseudonymization Techniques"
description: "The five core techniques for processing personal information into pseudonymized data that balances data utility with privacy."
icon: "visibility_off"
date: "2026-08-18"
lastmod: "2026-08-18"
draft: false
---

## I. Overview

```mermaid
%%{init: { 'theme': 'base', 'themeVariables': { 'edgeLabelBackground': '#fff' }}}%%
flowchart LR
    A["Identifiable\ninformation"] -- "applying the 5 core\npseudonymization techniques" --> B["Pseudonymized\n(de-identified) data"]
    style A fill:#f9f9f9,stroke:#333,stroke-width:3px
    style B fill:#e1f5fe,stroke:#01579b,stroke-width:3px
```

**Definition**: Pseudonymization techniques are technical methods that delete or substitute part of personal information so that a specific individual cannot be identified without additional information.

**Core value and purpose**:  
( **Data Utility** ) Preserves the data's statistical properties and quality ( **Utility** ) so it still fits the intended analysis purpose.  
( **Privacy Protection** ) Minimizes re-identification risk to safeguard data subjects' privacy rights.  
( **Risk Management** ) Secures legal compliance through technical measures and cuts off the risk of a security incident (re-identification) at the source.

## II. Mechanism & Components

### The 5 Core Pseudonymization Techniques and Their Sub-Methods

```mermaid
flowchart LR
    A["Original\npersonal information"] --> T1["1. Deletion"]
    A --> T2["2. Rounding"]
    A --> T3["3. Masking"]
    A --> T4["4. Substitution"]
    A --> T5["5. Aggregation"]

    T1 --> B["Pseudonymized data\nbalancing Utility\nand Privacy"]
    T2 --> B
    T3 --> B
    T4 --> B
    T5 --> B
```

| Pseudonymization Technique | Detailed Description | Concrete Example |
|-------------|---------|-----------|
| 1. Deletion | Directly deletes fields containing identifiers, or removes specific items | Fully deleting name, resident registration number, phone number |
| 2. Rounding | Converts numerical data into a range (bucket) or rounds it | Age 26 → "20s"; salary 3.54 million won → "3-4 million won" |
| 3. Masking | Replaces part of the data with a special character such as an asterisk (*) to prevent identification | Hong Gil-dong → Hong *dong; Gangnam-gu, Seoul → **-gu, Seoul |
| 4. Substitution | Replaces an identifier with an arbitrary unique or virtual number | Resident registration number → replaced with a serial number (A-001) |
| 5. Aggregation | Processes data as a group total or average rather than individual records | Individual income → converted to average income by department |

## III. Advanced Topics & Comparison

Pseudonymization techniques are more often mixed according to the characteristics of the data than used alone, and the following privacy-protection models are compared when applying them.

| Comparison Item | k-Anonymity | l-Diversity | t-Closeness |
|----------|----------------------|----------------------|----------------------|
| Core Concept | Keeps at least k records sharing the same attributes | Requires at least l distinct sensitive values within each k-group | Minimizes the difference between the overall attribute distribution and a specific group's distribution |
| Threat Defended | Linking attack | Homogeneity attack, background-knowledge attack | Skewness attack, similarity attack |
| Limitation | Vulnerable to homogeneity attacks | May reduce data utility | Complex and costly to implement |

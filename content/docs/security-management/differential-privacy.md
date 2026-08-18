---
weight: 5140
title: "Differential Privacy"
description: "A mathematically provable privacy mechanism that injects statistical noise so results barely change whether or not any one individual's data is included."
icon: "blur_on"
date: "2026-08-18"
lastmod: "2026-08-18"
draft: false
---

## I. Overview

```mermaid
%%{init: { 'theme': 'base', 'themeVariables': { 'edgeLabelBackground': '#fff' }}}%%
flowchart LR
    A["Individual record\nincluded (Data D)"] -- "injecting mathematical\nnoise (ε)" --> B["Statistically similar\nresult (Data D')"]
    style A fill:#f9f9f9,stroke:#333,stroke-width:3px
    style B fill:#e1f5fe,stroke:#01579b,stroke-width:3px
```

**Definition**: Differential privacy is a privacy-protection mechanism that injects mathematical noise into a probability distribution so that a statistical analysis result is nearly identical regardless of whether any one individual's data is included in the dataset.

**Core principle and features**:  
( **Defense against background-knowledge attacks** ) Mathematically proves that a specific individual cannot be identified even if an attacker holds external (background) information.  
( **Privacy budget** ) The smaller the value of `ε` ( **Privacy Budget** ), the stronger the privacy protection — but the lower the utility of the data, creating a trade-off.  
( **Mathematical rigor** ) The degree of privacy exposure is quantitatively controlled through a formula such as `Pr[M(D) ∈ S] ≤ e^ε × Pr[M(D') ∈ S]`.

## II. Mechanism & Components

### Implementation Models by Noise-Injection Location

```mermaid
flowchart LR
    U1["User\nRaw Data"] -->|"local noise injection\nLDP"| AGG1["Aggregation server\nno trust required"]
    AGG1 --> R1["Statistical result\nhigher security, lower accuracy"]

    U2["User\nRaw Data"] --> AGG2["Central server\nTrusted Curator"]
    AGG2 -->|"global noise injection\nGDP"| R2["Statistical result\nhigher accuracy, lower security"]
```

> **Key point**: Differential privacy is divided into the **local method (LDP)**, where noise is added on the user's device, and the **global method (GDP)**, where noise is added at the collecting central database.

### Key Components and Techniques

| Component | Detailed Description | Note |
|----------|---------|------|
| Privacy Budget (ε) | The tolerance range allowed for data exposure. The smaller it is, the higher the security and the lower the accuracy | Core tuning parameter |
| Laplace Mechanism | Adds Laplace-distribution-based noise to the data | Suited to numerical data |
| Sensitivity | The maximum change a single record can cause in a query result | Determines the size of the noise |
| Exponential Mechanism | Selects the optimal answer when responding with non-numerical (categorical) data | Applied to categorical data |

## III. Advanced Topics & Comparison

### Differential Privacy vs. the k-Anonymity Model

| Comparison Item | k-Anonymity Family | Differential Privacy |
|----------|--------------------------|-------------------------------------|
| Mathematical Definition | Empirical/structural de-identification (transforming values) | Based on rigorous mathematical proof (controlling the probability distribution) |
| Attack Defense | Defends against linking attacks and re-identification attacks | Robust against background-knowledge attacks |
| Data Form | Structured datasets (micro-data) | Query responses and statistics (statistical output) |
| Limitation | Re-identification risk persists, weak against high-dimensional data | Data accuracy degrades due to noise injection |

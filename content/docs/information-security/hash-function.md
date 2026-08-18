---
weight: 1130
title: "Hash Function"
description: "The one-way function that fingerprints data by converting an arbitrary-length message into a fixed-length digest."
icon: "fingerprint"
date: "2026-08-18"
lastmod: "2026-08-18"
draft: false
---

## I. Overview

```mermaid
%%{init: { 'theme': 'base', 'themeVariables': { 'edgeLabelBackground': '#fff' }}}%%
flowchart LR
    A["Message of\narbitrary length"] -- "One-way compression function" --> B["Fixed-length\ndigest"]
    style A fill:#f9f9f9,stroke:#333,stroke-width:3px
    style B fill:#e1f5fe,stroke:#01579b,stroke-width:3px
```

**Definition**: A one-way function that takes a message of arbitrary length as input and converts it into a fixed-length bit string (hash value).

**Features**:  
( **One-Way** ) Computing the hash value from the input is easy, but recovering the input from the hash value is infeasible  
( **Avalanche Effect** ) Even a tiny change to the input produces a completely different output hash value  
( **Compression** ) Regardless of the length of the input, the function always produces a hash value of a fixed, predetermined length  

## II. Mechanism & Components

### A. Three Core Security Properties of Hash Functions

| Security Property | Description | Note |
|:---:|----------|----------|
| 1. **Preimage Resistance** | For a given hash value `h`, it is difficult to find an input `x` such that `H(x) = h` | Guarantees one-wayness |
| 2. **Second Preimage Resistance** | For a given input `x`, it is difficult to find a different input `x'` such that `H(x) = H(x')` | Prevents tampering with an existing document |
| 3. **Collision Resistance** | It is difficult to find any two distinct inputs `x` and `x'` such that `H(x) = H(x')` | Guarantees signature integrity |

### B. Comparison of Major Hash Algorithms

| Algorithm | Hash Length (bits) | Features & Security Level |
|:---:|:---:|-----------------|
| **MD5** | 128 | Deprecated after collision-resistance flaws were discovered |
| **SHA-1** | 160 | Deprecated after forgery/tampering vulnerabilities were discovered |
| **SHA-2** | 224 / 256 / 384 / 512 | Currently the most widely used standard (e.g., **SHA-256**) |
| **SHA-3** | 224 / 256 / 384 / 512 | Based on the Keccak algorithm; offers structural robustness beyond SHA-2 |

## III. Advanced Topics & Comparison

### A. Key Use Cases
- **Integrity verification**: Confirming that an original file has not been tampered with when distributing software
- **Password storage**: Storing hash values instead of plaintext passwords to minimize damage in a breach (must be paired with **salting**)
- **Digital signatures**: Signing the hash value rather than encrypting the entire message, improving computational efficiency

### B. Attack Techniques and Countermeasures
- **Rainbow table** attacks: Use precomputed tables of hash values → countered with **salting** and **key stretching**
- **Birthday attack**: Exploits hash collisions → countered by using a sufficiently long hash length (256 bits or more)

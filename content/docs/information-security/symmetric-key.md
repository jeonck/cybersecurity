---
weight: 1210
title: "Symmetric-Key Cryptography"
description: "The core mechanism for high-speed data protection, built on a single secret key shared by sender and receiver."
icon: "password"
date: "2026-08-18"
lastmod: "2026-08-18"
draft: false
---

## I. Overview

```mermaid
%%{init: { 'theme': 'base', 'themeVariables': { 'edgeLabelBackground': '#fff' }}}%%
flowchart LR
    A["Plaintext"] -- "High-speed computation with a single secret key" --> B["Ciphertext"]
    style A fill:#f9f9f9,stroke:#333,stroke-width:3px
    style B fill:#e1f5fe,stroke:#01579b,stroke-width:3px
```

**Definition**: A cryptographic scheme in which sender and receiver use a pre-shared "**single secret key**" to transform plaintext into ciphertext, and back again into plaintext.

**Features**:  
( **High-Speed Computation** ) Computation is far faster than asymmetric-key cryptography  
( **Simple Structure** ) The algorithm structure is simple, making software and hardware implementation easy  
( **Efficiency** ) High computational efficiency makes it well suited to processing large volumes of data and real-time encryption  

## II. Mechanism & Components

### A. Structure of Symmetric-Key Cryptography

- **Encryption**: `C = E(K, P)` (P: plaintext, K: shared key, C: ciphertext)
- **Decryption**: `P = D(K, C)` (the same key K is used for both encryption and decryption)

### B. Classification by Data Processing Unit

| Category | Stream Cipher | Block Cipher |
|------|---------------------------|------------------------|
| **Processing Unit** | 1 bit or 1 byte at a time | Fixed-size blocks (64/128/256 bits) |
| **Core Principle** | Pseudorandom stream XORed with the data | Repeated **substitution (S)** and **permutation (P)** |
| **Computation Speed** | Very fast (real-time capable) | Relatively slower than a stream cipher |
| **Examples** | RC4, A5/1, Salsa20 | DES, AES, SEED, ARIA |
| **Trade-offs** | Easy hardware implementation, low diffusion | Higher security, but requires padding |

## III. Vulnerabilities & Security Measures

| Limitation | Details | Solution |
|:---:|----------|----------|
| **Key Distribution Problem** | Safely delivering the key to the recipient is difficult | Diffie-Hellman, hybrid cryptography (envelope) |
| **Key Management Burden** | `n(n-1)/2` keys are required among `n` users | KDC (key distribution center), integration with accredited certification systems |
| **Lack of Integrity** | Exposure of the key threatens not just confidentiality but also tampering | Use authenticated encryption such as HMAC or GCM mode |

The integrity gap is the limitation most likely to be silently overlooked in an implementation review — teams reliably remember to solve key distribution because it blocks basic functionality, but plain CBC or ECB mode encryption with no MAC ships more often than it should, leaving tampering undetected even though confidentiality looks fine on paper. Authenticated encryption (GCM, or encrypt-then-MAC) should be the non-negotiable default, not an opt-in hardening step.

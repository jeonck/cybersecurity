---
weight: 1070
title: "Asymmetric-Key Cryptography"
description: "A trust-based dual-key cryptographic system built on a mathematically linked public key and private key pair."
icon: "key"
date: "2026-08-18"
lastmod: "2026-08-18"
draft: false
---

## I. Overview

```mermaid
%%{init: { 'theme': 'base', 'themeVariables': { 'edgeLabelBackground': '#fff' }}}%%
flowchart LR
    A["Symmetric keys\nrequire pre-sharing"] -- "Using a public/private key pair" --> B["Key distribution\nproblem solved"]
    style A fill:#f9f9f9,stroke:#333,stroke-width:3px
    style B fill:#e1f5fe,stroke:#01579b,stroke-width:3px
```

**Definition**: A cryptographic scheme that uses a pair of keys — a **public key** and a **private key** — generated from a hard mathematical problem such as integer factorization or the discrete logarithm problem.

**Features**:  
( **Easy Key Distribution** ) The public key can be distributed openly, making key management far simpler than with symmetric-key cryptography  
( **Confidentiality and Non-repudiation** ) Alongside confidentiality through data encryption, it provides non-repudiation via digital signatures  
( **Computational Complexity** ) Because it relies on complex operations grounded in hard mathematical problems, it is relatively slower than symmetric-key cryptography  

## II. Mechanism & Components

### A. Confidentiality and Authentication (Digital Signature) Process

```mermaid
graph TD
    subgraph "Confidentiality"
        A1["Sender"] -->|"Encrypt with recipient's public key"| B1["Ciphertext"]
        B1 -->|"Decrypt with recipient's private key"| C1["Recipient (confidentiality achieved)"]
    end

    subgraph "Authentication & Non-repudiation"
        A2["Sender"] -->|"Encrypt with sender's private key"| B2["Digital signature"]
        B2 -->|"Decrypt with sender's public key"| C2["Verification (identity confirmed)"]
    end
```

**Detailed mechanism**:
- **Confidentiality**: Encrypted with the recipient's public key → only decryptable with the recipient's private key
- **Authentication and non-repudiation**: Encrypted (signed) with the sender's private key → anyone can decrypt (verify) it with the sender's public key

### B. Major Algorithms and Their Mathematical Hard Problems

| Algorithm | Underlying Hard Problem | Features & Use |
|----------|----------------|-------------|
| **RSA** | Integer factorization | The most widely used algorithm; key lengths trend longer over time (2048 bits or more) |
| **ECC** | Elliptic Curve Discrete Logarithm Problem (ECDLP) | Provides the same security strength as RSA with a much shorter key (ideal for mobile/IoT) |
| **Diffie-Hellman** | Discrete logarithm | A key-exchange-only algorithm, used in the early stages of SSL/TLS |
| **ElGamal** | Discrete logarithm | Has the drawback that ciphertext grows to twice the size of the plaintext |

## III. Advanced Topics & Comparison

| Comparison Item | Symmetric-Key Cryptography | Asymmetric-Key Cryptography |
|----------|------------|--------------|
| **Number of Keys** | 1 (shared secret key) | 2 (public key, private key) |
| **Key Distribution** | Difficult (requires pre-sharing) | Very easy (public key can be distributed) |
| **Computation Speed** | Fast (suited to large volumes) | Slow (roughly 100–1,000x slower) |
| **Core Use** | Encrypting the data body | Key exchange, digital signatures, authentication |

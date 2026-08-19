---
weight: 1190
title: "RSA Encryption"
description: "The number-theory-based trust scheme built on the fact that multiplying two primes is easy but factoring the product back out is hard."
icon: "vpn_key"
date: "2026-08-18"
lastmod: "2026-08-18"
draft: false
---

## I. Overview

```mermaid
%%{init: { 'theme': 'base', 'themeVariables': { 'edgeLabelBackground': '#fff' }}}%%
flowchart LR
    A["Multiplying two large\nprimes is easy"] -- "Factoring the product back out is hard" --> B["Public-key\ntrust scheme"]
    style A fill:#f9f9f9,stroke:#333,stroke-width:3px
    style B fill:#e1f5fe,stroke:#01579b,stroke-width:3px
```

**Definition**: A public-key algorithm built on the fact that multiplying two prime numbers together is easy, but recovering the original primes from that product is hard.

**Features**: In addition to confidentiality, RSA provides authentication and non-repudiation through digital signatures, and a key length of 2048 bits or more is recommended depending on the data.

```mermaid
flowchart LR
    RSA["RSA public-key\ncryptography"] --> C["Confidentiality\nencrypt with recipient's public key"]
    RSA --> S["Authentication · non-repudiation\nsign with sender's private key"]
    RSA --> K["Key exchange\ndeliver an encrypted session key"]

    C --> C1["Decrypt with recipient's private key"]
    S --> S1["Verify signature with sender's public key"]
    K --> K1["Hybrid encryption\n(RSA + AES)"]
```

## II. Mechanism & Components

### A. Key Generation and Encryption/Decryption

**Key generation procedure**:

1. Choose two large primes `p` and `q`, and compute `n = p × q`
2. Compute Euler's totient: `φ(n) = (p-1)(q-1)`
3. Choose a public exponent `e` that is coprime to `φ(n)`
4. Compute a private exponent `d` satisfying `e × d ≡ 1 (mod φ(n))`
5. **Public key**: `(e, n)` / **Private key**: `(d, n)`

| Operation | Formula |
|-----|------|
| Encryption | `C = M^e mod n` |
| Decryption | `M = C^d mod n` |

```mermaid
sequenceDiagram
    participant A as "Sender (Alice)"
    participant B as "Recipient (Bob)"

    Note over B: "Key generation<br/>public key (e, n) published<br/>private key (d, n) kept secret"
    B-->>A: "Deliver public key (e, n)"
    Note over A: "Encryption<br/>C = M^e mod n"
    A->>B: "Send ciphertext C"
    Note over B: "Decryption<br/>M = C^d mod n"
```

### B. Key Security Properties of RSA

| Item | Details |
|-----|---------|
| Security Basis | The integer-factorization problem — extracting `p` and `q` from an `n` of several thousand bits or more is computationally infeasible |
| Use 1: Confidentiality | Encrypted with the recipient's public key → decrypted with the recipient's private key |
| Use 2: Authentication | Encrypted (signed) with the sender's private key → verified with the sender's public key |
| Constraint | Slower than symmetric-key cryptography, so it is used mainly for "session key encryption" or "signing" only |

## III. Vulnerabilities & Security Measures

```mermaid
flowchart TD
    LIM["RSA limitations"] --> L1["Computation speed and key length"]
    LIM --> L2["Chosen-ciphertext attack (CCA)"]
    LIM --> L3["Quantum computing threat"]

    L1 -->|"Response"| R1["Migrate to ECC (elliptic curve cryptography)\nsame security strength, shorter keys"]
    L2 -->|"Response"| R2["Apply OAEP padding\n(blocks attacks by mixing in randomness)"]
    L3 -->|"Response"| R3["Adopt PQC (post-quantum cryptography)\nto prepare against Shor's algorithm"]
```

| Limitation | Response |
|------|---------|
| Computation speed and key length | Migrate to **ECC (elliptic curve cryptography)**, which offers better computational efficiency for the same security strength |
| Chosen-ciphertext attack (CCA) | Apply **OAEP**, a padding technique that mixes randomness into the data |
| Quantum computing threat | Can be defeated by Shor's algorithm → adoption of **PQC (post-quantum cryptography)** is required |

Textbook (unpadded) RSA is the vulnerability practitioners are most likely to reintroduce by accident, not the quantum threat — any implementation or library defaulting to raw RSA without OAEP padding is exploitable today via chosen-ciphertext attacks, while the quantum threat still has a migration runway ahead of it. Audit for correct padding usage first; treat the PQC transition as the longer-horizon project it actually is.

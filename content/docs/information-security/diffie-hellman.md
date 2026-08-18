---
weight: 1100
title: "Diffie-Hellman Key Exchange"
description: "The algorithm that solved the key distribution problem by deriving a shared secret over a public channel using the discrete logarithm problem."
icon: "sync_alt"
date: "2026-08-18"
lastmod: "2026-08-18"
draft: false
---

## I. Overview

```mermaid
%%{init: { 'theme': 'base', 'themeVariables': { 'edgeLabelBackground': '#fff' }}}%%
flowchart LR
    A["Public channel\n(insecure channel)"] -- "Key derivation via discrete logarithm" --> B["Shared secret key"]
    style A fill:#f9f9f9,stroke:#333,stroke-width:3px
    style B fill:#e1f5fe,stroke:#01579b,stroke-width:3px
```

**Definition**: A cryptographic algorithm that, based on the computational difficulty of the discrete logarithm problem, allows communicating parties to derive a common secret key over a public channel without ever sharing their private keys.

**Key Features**:  
( **Solves the Key Distribution Problem** ) A session key can be derived securely without needing to share a key in advance  
( **The First Public-Key-Based Scheme** ) Published in 1976, it was the first public-key cryptographic algorithm and the starting point of modern cryptography  
( **Based on the Discrete Logarithm** ) Relies on the mathematical principle that reversing exponentiation over a finite field is computationally hard  

## II. Mechanism & Components

### A. Key Exchange Process (Alice & Bob)

```mermaid
sequenceDiagram
    participant A as "Alice"
    participant B as "Bob"

    Note over A,B: "① Agree on common parameters (public)<br/>choose prime p, generator g"
    A->>A: "② Generate private key a (secret)<br/>compute A = g^a mod p"
    B->>B: "② Generate private key b (secret)<br/>compute B = g^b mod p"
    A->>B: "③ Send public value A"
    B->>A: "③ Send public value B"
    A->>A: "④ Compute K = B^a mod p"
    B->>B: "④ Compute K = A^b mod p"
    Note over A,B: "Shared secret key K = g^ab mod p is derived"
```

**Step-by-step description**:

1. **Agree on common parameters**: A large prime `p` and a generator `g` are chosen publicly
2. **Generate private keys**: Alice generates a random private key `a`, and Bob generates `b` (both secret)
3. **Compute and exchange public values**:
   - Alice computes `A = g^a mod p` and sends it to Bob
   - Bob computes `B = g^b mod p` and sends it to Alice
4. **Derive the shared secret key**:
   - Alice computes `K = B^a mod p = (g^b)^a mod p`
   - Bob computes `K = A^b mod p = (g^a)^b mod p`
   - As a result, both sides hold the identical `K = g^ab mod p`

### B. Security Characteristics

| Item | Description |
|-----|------|
| Mathematical Basis | The discrete logarithm problem — even knowing `Y` in `g^x mod p = Y`, computing `x` is computationally infeasible |
| Perfect Forward Secrecy (PFS) | When ephemeral keys are used, past communications cannot be decrypted even if the server's long-term private key is later compromised |
| Weakness | Vulnerable to **man-in-the-middle (MitM) attacks** — since it provides no authentication, the identity of the other party cannot be confirmed |

## III. Advanced Topics & Comparison

```mermaid
flowchart LR
    DH["Basic DH\n(Diffie-Hellman)"] -->|"Key reuse problem"| DHE["DHE\n(DH Ephemeral)\none-time key per session"]
    DHE -->|"Computation cost problem"| ECDHE["ECDHE\n(Elliptic Curve DHE)\nshort keys · fast computation"]

    DH -.->|"Vulnerable to MitM"| WARN["No authentication\n→ must be combined with certificates (PKI)"]
    ECDHE -->|"Modern TLS standard"| TLS["TLS 1.3\ndefault key exchange algorithm"]
```

| Model | Features | Security Strength | Status |
|-----|------|---------|------|
| DH | Fixed key use, simple implementation | Low (key reuse) | Legacy |
| DHE | Generates an ephemeral key each session → provides PFS | High | Recommended |
| ECDHE | Applies elliptic-curve (ECC) cryptography → same security strength with shorter keys, faster computation | Very high | **Modern TLS standard** |

> **Key point**: ECDHE delivers both high security strength and PFS with a short key length (256-bit ≈ RSA 3072-bit), which is why it was adopted as the default key exchange method in TLS 1.3.

---
weight: 2170
title: "TLS (Transport Layer Security)"
description: "The transport-layer security protocol (RFC 8446) that establishes an encrypted channel between client and server to guarantee confidentiality, integrity, and authentication."
icon: "https"
date: "2026-08-18"
lastmod: "2026-08-18"
draft: false
---

## I. Overview

```mermaid
%%{init: { 'theme': 'base', 'themeVariables': { 'edgeLabelBackground': '#fff' }}}%%
flowchart LR
    A["Plaintext comms and\nweak legacy SSL"] -- "Confidentiality, integrity, and\nhandshake overhead optimized" --> B["Hardened, high-performance\nTLS (especially 1.3)"]
    style A fill:#f9f9f9,stroke:#333,stroke-width:3px
    style B fill:#e1f5fe,stroke:#01579b,stroke-width:3px
```

**Definition**: A transport-layer security protocol ( **RFC 8446** ) that establishes an encrypted channel between a client and a server to guarantee the confidentiality, integrity, and authentication of data in internet communications.

**Features**:  
( **Hybrid Cryptosystem** ) Uses public-key cryptography ( **Asymmetric** ) to safely exchange a symmetric key, then transmits the actual data using fast symmetric-key encryption ( **Symmetric** ).  
( **Integrity Assurance** ) Uses a message authentication code ( **MAC** ) or **HMAC** to verify in real time whether data has been tampered with in transit.  
( **Strong Authentication** ) Uses digital certificates ( **X.509** ) and the **PKI** system to verify the identity of the communicating party and prevent man-in-the-middle attacks ( **MITM** ).  
( **Performance Optimization** ) The latest **TLS 1.3** shortens the handshake ( **1-RTT**, **0-RTT** ), achieving both security and speed.

## II. Mechanism & Components

### TLS 1.3 Handshake Flow (1-RTT)

```mermaid
sequenceDiagram
    participant C as "Client"
    participant S as "Server"

    Note over C,S: "1. Client Hello (supported algorithms, Key Share)"
    C->>S: "Client Hello"

    Note over S,C: "2. Server Hello (algorithm confirmed, Certificate, Finished)"
    S-->>C: "Server Hello + Encrypted Extensions + Certificate + Finished"

    Note over C,S: "3. Certificate verification and start of data transmission"
    C->>S: "Finished (Encrypted)"

    Note over C,S: "4. Secure Application Data Exchange"
    C->>S: "Application Data (Encrypted)"
    S->>C: "Application Data (Encrypted)"
```

### The Four Sub-Protocols That Make Up TLS

| Protocol | Detailed Description | Primary Role |
|:---:|----------|----------|
| **Handshake** | Negotiates the encryption algorithm ( **Cipher Suite** ) and generates the session key | Mutual authentication and agreement on security parameters |
| **Change Cipher Spec** | Notifies that subsequent messages will be sent using the negotiated cipher spec | Notification of the switch to encrypted mode |
| **Alert** | Communicates errors or risk conditions that occur during communication | Error handling and session termination control |
| **Record** | The basic unit that fragments, compresses, and encrypts actual data for transmission | Data encapsulation and integrity protection |

## III. Expected Benefits & Implications

Deprecating TLS 1.2 in favor of 1.3 isn't just a performance upgrade — it removes an entire category of downgrade and cipher-negotiation attacks by simply not allowing the weak options (static RSA/DH key exchange, plaintext handshake portions) to exist on the wire at all. The real-world payoff of PFS in particular is easy to underrate until a private key does eventually leak: without it, that single leak retroactively decrypts every past session ever captured, while with it the blast radius is one session.

| Benefit | Where It Shows Up |
|---|---|
| Faster handshake (1-RTT/0-RTT) | User-perceived latency, mobile performance |
| Eliminated downgrade attack surface | Reduced exposure to MITM interception |
| Forward secrecy by default | Bounded blast radius if a private key is later compromised |

Budget SNI encryption (ECH) as the next adoption target, not TLS 1.3 itself — plenty of environments have already completed the 1.2-to-1.3 migration but still leak the destination hostname in plaintext, which is exactly the kind of half-finished hardening that gives a false sense of completion.

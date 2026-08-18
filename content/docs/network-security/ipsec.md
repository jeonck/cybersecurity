---
weight: 2140
title: "IPSec"
description: "A protocol suite that establishes an encrypted, authenticated security channel at the network layer (L3) for data carried over IP networks."
icon: "vpn_lock"
date: "2026-08-18"
lastmod: "2026-08-18"
draft: false
---

## I. Overview

```mermaid
%%{init: { 'theme': 'base', 'themeVariables': { 'edgeLabelBackground': '#fff' }}}%%
flowchart LR
    A["Untrusted\nIP network"] -- "Establishes a secure channel (ESP/AH)" --> B["Secure tunnel\n(VPN)"]
    style A fill:#f9f9f9,stroke:#333,stroke-width:3px
    style B fill:#e1f5fe,stroke:#01579b,stroke-width:3px
```

**Definition**: A protocol suite that establishes a security channel at the network layer ( **L3** ) through encryption and authentication between communicating parties when transmitting data over an **IP** network.

**Features**:  
( **Confidentiality** ) Encrypts data via **ESP** ( **Encapsulating Security Payload** ).  
( **Integrity** ) Prevents tampering via **AH** ( **Authentication Header** ) and **ESP** authentication.  
( **Authentication** ) Confirms the identity of communicating entities and exchanges keys via the **IKE** ( **Internet Key Exchange** ) protocol.  
( **Availability** ) Uses sequence numbers ( **Sequence Number** ) to prevent replay attacks ( **Replay Attack** ).

## II. Mechanism & Components

### IPSec Protocol Stack Structure

```mermaid
flowchart TD
    subgraph IKE["IKE (Internet Key Exchange)"]
        IK["Negotiates security policy (SA)\nManages encryption key exchange"]
    end

    subgraph AH["AH (Authentication Header)"]
        AH1["Authenticates header + data,\nensures integrity — no confidentiality"]
    end

    subgraph ESP["ESP (Encapsulating Security Payload)"]
        ESP1["Encrypts data for confidentiality,\nincludes optional authentication"]
    end

    IKE -->|"After SA is established"| AH
    IKE -->|"After SA is established"| ESP
```

| Protocol | Function | Confidentiality | Integrity | Authentication |
|--------|------|:-----:|:-----:|:----:|
| AH | Header + data authentication | ✕ | ✓ | ✓ |
| ESP | Data encryption + optional authentication | ✓ | ✓ | ✓ |
| IKE | SA negotiation and key exchange | — | — | ✓ |

### Transport Mode vs. Tunnel Mode

```mermaid
flowchart LR
    subgraph TM["Transport Mode"]
        direction LR
        T1["Original IP Header"] --- T2["AH/ESP Header"] --- T3["Data (Payload)"]
    end

    subgraph TUN["Tunnel Mode"]
        direction LR
        N1["New IP Header"] --- N2["AH/ESP Header"] --- N3["Original IP Header"] --- N4["Data"]
    end
```

| Category | Transport Mode | Tunnel Mode |
|-----|--------------------------|----------------------|
| Protected Scope | The data (payload) portion of the IP packet | The entire IP packet (header + data) |
| Header Structure | Uses the original IP header as-is | Adds a **new IP header** |
| Primary Use | Host-to-host (end-to-end) communication | Site-to-site VPN |
| Characteristics | Lower overhead, but the original IP is exposed | Higher security, enables private IP communication |

## III. Advanced Topics & Comparison

### IPSec Security Policy Management: SPD and SAD

```mermaid
flowchart LR
    PKT["Incoming Packet"] -->|"SPI lookup"| SPD["SPD\nSecurity Policy DB\nDetermines traffic handling policy"]
    SPD -->|"Requires protection"| SAD["SAD\nSecurity Association DB\nManages keys and algorithm info"]
    SAD -->|"Applies SA"| DEC["Decryption / Authentication"]
    SPD -->|"Passes through"| PASS["Passed through as-is"]
    SPD -->|"Discarded"| DROP["Packet discarded"]
```

| Element | Detailed Description | Notes |
|-----|---------|------|
| SPD (Security Policy DB) | A policy database that decides which traffic to process for security | Determines protect / pass / discard |
| SAD (Security Association DB) | Manages the encryption keys and algorithm information for currently active SAs | Active security information |
| SPI (Index) | An index value that identifies which SA an incoming packet corresponds to | Included in the packet header |

> **Key Point**: **IPSec** operates at the network layer (L3), so it can apply security transparently without requiring changes to upper-layer applications, and it serves as the core underlying technology for VPN implementations.

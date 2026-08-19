---
weight: 2150
title: "OSI 7-Layer Security"
description: "A framework that analyzes the security threats specific to each OSI-model layer and applies matching security technologies and solutions at that layer."
icon: "layers"
date: "2026-08-18"
lastmod: "2026-08-18"
draft: false
---

## I. Overview

```mermaid
%%{init: { 'theme': 'base', 'themeVariables': { 'edgeLabelBackground': '#fff' }}}%%
flowchart LR
    A["Single, undifferentiated\nsecurity control"] -- "Layer-specific security applied" --> B["Defense-in-depth\nsystem built"]
    style A fill:#f9f9f9,stroke:#333,stroke-width:3px
    style B fill:#e1f5fe,stroke:#01579b,stroke-width:3px
```

**Definition**: A framework that analyzes the security threats specific to each of the seven network layers defined by the International Organization for Standardization ( **ISO** ) and applies matching security technologies and solutions to counter them.

**Features**:  
( **Layered Security** ) Implements a multi-layer defense system in which a threat is still blocked at another layer even if a specific layer is compromised.  
( **Visibility** ) Provides fine-grained control over network traffic through protocol analysis at each layer.  
( **Accountability** ) Enables precise identification of where a fault or security incident occurred, allowing for rapid response.

## II. Mechanism & Components

### OSI 7-Layer Security Architecture

- **Lower Layers** (Physical / Data Link): Handle physical connectivity and security between adjacent nodes.
- **Upper Layers** (Transport / Application): Control end-to-end encryption and data visibility.

### Security Activities and Core Protocols by Layer

| Layer | Primary Security Threat | Countermeasure Technology/Protocol | Security Equipment / Solution |
|:---:|--------------|--------------------|-----------------|
| **7. Application** | SQL Injection, XSS, HTTP Flooding | S-HTTP, PGP / S-MIME, DNSSEC | WAF, Anti-Spam |
| **6. Presentation** | Data tampering, decryption attacks | Format verification, encryption / compression | - |
| **5. Session** | Session Hijacking | SSH, RPC security | - |
| **4. Transport** | Port Scanning, SYN Flooding | SSL / TLS, WTLS | FW, Load Balancer |
| **3. Network** | IP Spoofing, ICMP Flooding | IPSec (AH, ESP), VPN | Router ACL, IPS |
| **2. Data Link** | MAC Flooding, ARP Spoofing | 802.1x, MAC filtering | L2 / L3 security switch |
| **1. Physical** | Eavesdropping (Tapping), physical destruction | Physical shielding, port locking | CCTV, fingerprint recognition |

## III. Outlook & Future Direction

| Security Focus | Maturity | Direction |
|---|---|---|
| L3/L4 perimeter blocking (ACL, firewall) | Legacy baseline | Still necessary, no longer sufficient alone |
| L7 DPI and SSL-visibility inspection | Mainstream | Required as encrypted traffic share keeps growing |
| Zero Trust applied across all layers | Emerging | Becoming the organizing principle, not just an L3/L4 control |

Layer-by-layer defense was built for an era when most traffic was inspectable in the clear — that era is over. With the overwhelming majority of traffic now running over TLS, a security architecture that stops at L3/L4 ACLs is effectively blind to whatever crosses L6/L7, which is exactly where modern attacks live. Expect SSL-visibility inspection to shift from an optional add-on to a baseline requirement, and expect "never trust, always verify" to stop being a separate L3/L4 control and instead become the lens every layer's security decisions get made through.

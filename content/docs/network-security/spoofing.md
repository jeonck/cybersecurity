---
weight: 2120
title: "Spoofing"
description: "An attack that forges network identifiers such as IP, MAC, or DNS to impersonate a trusted party and hijack a trust relationship."
icon: "badge"
date: "2026-08-18"
lastmod: "2026-08-18"
draft: false
---

## I. Overview

```mermaid
%%{init: { 'theme': 'base', 'themeVariables': { 'edgeLabelBackground': '#fff' }}}%%
flowchart LR
    A["Attacker"] -- "Impersonates trusted\nidentification info" --> B["Target\n(Target / System)"]
    style A fill:#f9f9f9,stroke:#333,stroke-width:3px
    style B fill:#e1f5fe,stroke:#01579b,stroke-width:3px
```

**Definition**: An attack technique that forges network identification information such as **IP** addresses, **MAC** addresses, and **DNS** names to masquerade as an authorized user, gaining system access or intercepting data.

**Features**:  
( **Exploiting Trust Relationships** ) Exploits the trust relationship ( **Trust Relationship** ) between systems to bypass authentication procedures or hijack privileges.  
( **Basis for Man-in-the-Middle Attacks** ) Redirects the flow of data packets to the attacker, serving as the core mechanism for eavesdropping ( **Sniffing** ) and tampering in man-in-the-middle attacks ( **MITM** ).  
( **Occurs Across Multiple Layers** ) Occurs at every layer, from the data link layer ( **ARP** ) to the network layer ( **IP** ) to the application layer ( **DNS** / **Email** ).

## II. Mechanism & Components

### ARP Spoofing Mechanism (L2 Layer)

```mermaid
sequenceDiagram
    participant A as "User A (Victim)"
    participant H as "Attacker (Hacker)"
    participant G as "Gateway (GW)"

    Note over H: "Sends a forged ARP reply posing as the gateway"
    H->>A: "ARP Reply (GW's IP is Hacker's MAC)"
    Note over H: "Sends a forged ARP reply posing as User A"
    H->>G: "ARP Reply (A's IP is Hacker's MAC)"
    Note over A,G: "All traffic now passes through the attacker"
    A->>H: "Packet to Internet"
    H->>G: "Forwarding to GW"
```

### Detailed Comparison of Major Spoofing Types

| Type | Forged Element | Attack Purpose | Core Mechanism |
|:---:|----------|----------|--------------|
| **IP Spoofing** | Source **IP** address | Filter evasion, hiding the origin of a **DDoS** attack | Tampering with the **Source IP** in the **IP** header |
| **ARP Spoofing** | **MAC** address | Eavesdropping on data within the local network ( **Sniffing** ) | Continuously sending forged **ARP Reply** packets |
| **DNS Spoofing** | **DNS** query response | Pharming ( **Pharming** ), redirection to phishing sites | Poisoning the **DNS** cache or pre-empting the legitimate response |
| **Email Spoofing** | Sender address | Social engineering attacks, spam/malware distribution | Forging sender information in the **SMTP** protocol |

## III. Vulnerabilities & Security Measures

| Spoofing Type | Underlying Weakness | Security Measure |
|---|---|---|
| ARP Spoofing | ARP has no built-in authentication | Static ARP/MAC pinning for critical hosts, Dynamic ARP Inspection |
| IP Spoofing | Source IP is trusted without verification | Ingress/egress filtering (BCP38) at the network boundary |
| DNS Spoofing | Cache poisoning / response pre-emption | DNSSEC to sign and verify DNS responses |
| Email Spoofing | SMTP sender fields are unauthenticated by design | SPF / DKIM / DMARC on the sending domain |

Every one of these defenses works by adding authentication to a protocol that was never designed to have any — which is also why none of them is optional or interchangeable with the others. DAI stops ARP spoofing on your own switch ports but does nothing for a spoofed DNS response, and DNSSEC does nothing for a spoofed email sender; treat spoofing defense as a checklist across protocols, not a single control to get right once.

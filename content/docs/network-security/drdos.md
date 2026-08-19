---
weight: 2080
title: "DRDoS (Distributed Reflective Denial of Service)"
description: "A denial-of-service attack that spoofs the victim's IP address to trick reflector servers into flooding the victim with amplified responses."
icon: "repeat"
date: "2026-08-18"
lastmod: "2026-08-18"
draft: false
---

## I. Overview

```mermaid
%%{init: { 'theme': 'base', 'themeVariables': { 'edgeLabelBackground': '#fff' }}}%%
flowchart LR
    A["Attacker\n(Spoofed IP)"] -- "Small request packet" --> B["Reflector Servers"]
    B -- "Amplified response packet" --> C["Target Server\n(Victim)"]
    style A fill:#f9f9f9,stroke:#333,stroke-width:3px
    style B fill:#fff9c4,stroke:#fbc02d,stroke-width:3px
    style C fill:#e1f5fe,stroke:#01579b,stroke-width:3px
```

**Definition**: An attack technique in which the attacker spoofs its own **IP** address as the victim's **IP** ( **Spoofing** ), sends requests to numerous reflector servers ( **Reflector** ), and has those servers concentrate amplified responses onto the victim, overwhelming it.

**Features**:  
( **Reflection and Amplification** ) Exploits characteristics of the **UDP** protocol to induce response packets tens to tens of thousands of times larger than the request — an amplification ( **Amplification** ) attack.  
( **Difficulty of Tracing** ) The attacker never sends packets directly but routes through servers providing legitimate services, making it extremely difficult to identify the true origin of the attack.  
( **Asymmetric Attack** ) With minimal resources (bandwidth), the attacker borrows the resources of reflector servers to inflict large-scale traffic damage on the victim.

## II. Mechanism & Components

### Reflection and Amplification Attack Process

```mermaid
sequenceDiagram
    participant A as "Attacker (Hacker)"
    participant R as "Reflector Servers"
    participant V as "Victim"

    Note over A: "Spoofs Source IP as the victim's IP"
    A->>R: "Sends small request packet (e.g. DNS Query)"
    Note over R: "Generates a normal response to the request"
    R->>V: "Flood of amplified response packets (DNS Response)"
    Note over V: "Availability exhausted, service disrupted"
```

### Major Reflection/Amplification Protocols and Amplification Factors

| Protocol | Primary Service | Amplification Factor (Max) | Detailed Mechanism |
|:---:|----------|:--------------:|--------------|
| **DNS** | Domain name resolution | About 50x | Returns a large-volume response to an `ANY` record request |
| **NTP** | Time synchronization | About 550x | Requests a list of recent connections via the `monlist` command |
| **SNMP** | Network management | About 6x | Bulk request for large volumes of device information |
| **SSDP** | Plug and play | About 30x | **UPnP** device discovery and information response |
| **Memcached** | Distributed memory cache | **About 50,000x** | Returns large volumes of cached data when the **UDP** port is exposed |

## III. Vulnerabilities & Security Measures

| Attack Vector | Root Vulnerability | Security Measure |
|---|---|---|
| Source IP spoofing | No verification that outbound packets carry a legitimate source address | Ingress/egress filtering (BCP38) at network boundaries |
| Open reflector services | UDP services (DNS, NTP, SNMP, SSDP, Memcached) reachable from the internet with no rate limiting | Close unnecessary UDP services, disable legacy features like NTP monlist |
| Domain-targeted floods | Attack traffic routed directly to the victim's published IP | DNS sinkhole redirecting to a cleansing facility |
| Sudden protocol-specific surges | No baseline for normal UDP 53/123/etc. volume | Threshold-based blocking tied to real traffic baselines |

Ingress filtering (BCP38) is the control every network security engineer agrees on and almost none of them can force upstream — DRDoS persists mainly because it weaponizes servers on networks the victim doesn't control. Treat "does our upstream provider filter spoofed source IPs" as a vendor-selection question, not just a configuration checkbox on your own routers, and don't assume closing your own reflector services protects you from being a victim of someone else's.

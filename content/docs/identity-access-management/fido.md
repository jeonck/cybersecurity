---
weight: 9040
title: "FIDO (Fast IDentity Online)"
description: "A passwordless authentication standard that uses biometrics and public-key cryptography to replace vulnerable, phishable passwords."
icon: "fingerprint"
date: "2026-08-18"
lastmod: "2026-08-18"
draft: false
---

## I. Overview

```mermaid
%%{init: { 'theme': 'base', 'themeVariables': { 'edgeLabelBackground': '#fff' }}}%%
flowchart LR
    A["Password-based\nauthentication"] -- "Biometrics and public-key cryptography" --> B["Convenient, strong\nauthentication"]
    style A fill:#f9f9f9,stroke:#333,stroke-width:3px
    style B fill:#e1f5fe,stroke:#01579b,stroke-width:3px
```

**Definition**: FIDO (Fast IDentity Online) is an authentication standard that replaces password-based login with device-held biometric verification and public-key cryptography.

**Features**:  
( **Stronger Security** ) Replaces passwords, which risk exposure, with biometric-based, public-key authentication — cutting off phishing and account-takeover attacks at the source  
( **Privacy Protection** ) Biometric data is never sent to the server; it stays only within the device's secure storage area, preventing leakage  
( **User Convenience** ) Authenticates quickly through a simple action such as a fingerprint or facial scan, with no complex password to type  

## II. Mechanism & Components

### A. FIDO Authentication Process (Registration & Authentication)

```mermaid
sequenceDiagram
    participant User as User (Client)
    participant Device as Authenticator
    participant Server as FIDO Server

    Note over Device: [Registration Phase]
    User->>Device: Provide biometric input
    Device->>Device: Generate private key, store in secure area (TEE)
    Device->>Server: Send and register public key

    Note over Device: [Authentication Phase]
    Server->>Device: Send challenge (random value)
    User->>Device: Provide biometric input
    Device->>Device: Sign challenge with private key (response)
    Device->>Server: Send signature value
    Server->>Server: Verify signature with registered public key
```

**Detailed steps**:
- **Registration**: After biometric authentication on the device, the resulting public key is registered with the server (the private key stays in the device's secure area, the TEE)
- **Authentication**: The device signs the challenge sent by the server using the private key and returns the response
- **Verification**: The server verifies the signature with the registered public key to confirm authentication success

### B. Key Differences Across FIDO Standard Versions

| Category | FIDO 1.0 (UAF / U2F) | FIDO 2.0 (WebAuthn) |
|:---:|---------------------|--------------------|
| **Primary Target** | Mainly mobile app environments | Web browser and PC environments |
| **UAF** | Login using biometrics alone (**Passwordless**) | - |
| **U2F** | An added security key on top of ID/PW (**2nd Factor**) | - |
| **Core Technology** | Requires a dedicated client app | **WebAuthn** (W3C standard API), **CTAP** |
| **Extensibility** | Tied to a specific OS / device | General-purpose, browser-based authentication |

## III. Adoption Outlook & Future Direction

| Generation | Status | Direction |
|---|---|---|
| FIDO 1.0 (UAF / U2F) | Legacy, app- or hardware-key dependent | Being phased out in favor of WebAuthn |
| FIDO2 / WebAuthn (single device) | Mature, broadly supported | Baseline capability, largely absorbed into passkeys |
| Passkey (synced FIDO2) | Rapidly growing platform default | Becoming the standard consumer sign-in method |

FIDO's own history shows why the passkey framing succeeded where FIDO 1.0 stalled: U2F and UAF solved the cryptography but still asked users to manage a device-bound credential, which is exactly the friction cloud sync removes. Expect FIDO2/WebAuthn to keep functioning as the underlying protocol while "passkey" becomes the user-facing product name — new deployments should target passkey UX flows rather than building against bare WebAuthn as an end state.

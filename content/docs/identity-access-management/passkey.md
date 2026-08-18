---
weight: 9110
title: "Passkey"
description: "A cloud-synced FIDO2 credential that completes the shift to passwordless authentication across a user's devices."
icon: "passkey"
date: "2026-08-18"
lastmod: "2026-08-18"
draft: false
---

## I. Overview

```mermaid
%%{init: { 'theme': 'base', 'themeVariables': { 'edgeLabelBackground': '#fff' }}}%%
flowchart LR
    A["Tied to\na single device"] -- "Cloud-synced FIDO2" --> B["A complete passwordless\nexperience"]
    style A fill:#f9f9f9,stroke:#333,stroke-width:3px
    style B fill:#e1f5fe,stroke:#01579b,stroke-width:3px
```

**Definition**: A passkey is a FIDO2-based credential that syncs across a user's devices via the cloud, completing the shift to a fully passwordless authentication experience.

**Features**:  
( **Passwordless** ) Eliminates passwords, which are hard to remember and easy to steal, fundamentally strengthening the authentication process  
( **Multi-Device Sync** ) Cloud-based credential sync provides continuity across a device change with no re-registration required  
( **Phishing Cut Off at the Source** ) Domain-binding technology automatically and technically rejects authentication requests from fake sites  

## II. Mechanism & Components

### A. Passkey Authentication Structure and Sync Process

```mermaid
graph TD
    subgraph "User Environment (Client)"
        D1["Smartphone\n(key generation)"] <--> Cloud["Cloud Sync\n(iCloud / Google)"]
        Cloud <--> D2["PC / Tablet"]
    end

    D1 -- "WebAuthn / CTAP2" --- Server["Service Server\n(Relying Party)"]
    D2 -- "WebAuthn / CTAP2" --- Server

    Comment["Biometric check, then a\nresponse signed with the private key"] -.-> D1
    Comment -.-> D2
```

- **Sync**: A generated passkey is automatically copied to the user's other devices on the same account via services like iCloud or Google Password Manager
- **Authentication**: The device signs the server's challenge with its private key and responds; the actual biometric data or password is never sent to the server

### B. Key Technical Elements of Passkeys

| Technical Element | Details | Note |
|:---:|----------|----------|
| **WebAuthn** | A standard API for performing FIDO authentication in a web browser | W3C standard |
| **CTAP2** | A communication protocol between an external authenticator (e.g., a smartphone) and a platform | Cross-device linkage |
| **End-to-End Encryption** | Encrypts credentials when syncing via the cloud | Not even the cloud provider can read them |
| **Multi-Device FIDO** | A credential created on one device can be used on other devices | The key differentiator of passkeys |

## III. Advanced Topics & Comparison

| Comparison Item | Password | Traditional FIDO (Single Device) | Passkey |
|----------|-------------------|--------------------------|-----------------|
| **User Experience** | Must be remembered and typed | Must be registered on each device | Register once, use on every device |
| **Security** | Vulnerable to phishing and brute force | Very high | Very high (blocks phishing at the source) |
| **On Device Loss** | Can be reset | Credential must be reissued | Recoverable via the cloud |
| **Core Philosophy** | Knowledge-based | Possession-based | Syncable credential |

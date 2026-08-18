---
weight: 4150
title: "Software Supply Chain Security (SBOM and SLSA)"
description: "The set of activities that manage security threats and ensure trustworthiness across the entire process from software production to delivery."
icon: "link"
date: "2026-08-18"
lastmod: "2026-08-18"
draft: false
---

## I. Overview

```mermaid
%%{init: { 'theme': 'base', 'themeVariables': { 'edgeLabelBackground': '#fff' }}}%%
flowchart LR
    A["Open-source threats"] -- "SBOM and SLSA\nframeworks" --> B["Assured software\ntrustworthiness"]
    style A fill:#f9f9f9,stroke:#333,stroke-width:3px
    style B fill:#e1f5fe,stroke:#01579b,stroke-width:3px
```

**Definition**: Software supply chain security refers to the activities that manage security threats and ensure trustworthiness across the entire process — design, development, build, and deployment — by which software is produced and delivered to users.

**Features**:  
( **Responding to Surging Threats** ) The need for a proactive defense system against supply chain attacks such as the Log4j and SolarWinds incidents.  
( **Ensuring Transparency** ) Securing visibility into software components (SBOM) to enable rapid response when a vulnerability arises.  
( **Ensuring Trustworthiness** ) Verifying integrity across the entire process, from development to deployment, to prevent the distribution of tampered software.

## II. Mechanism & Components

### A. Comparison of Major SBOM Standards

The SBOM (Software Bill of Materials) — a specification of a software's component parts — is primarily represented using the industry standard SPDX and the security-focused CycloneDX.

| Category | SPDX (ISO/IEC 5962) | CycloneDX |
|------|---------------------|-----------|
| Governing Body | Linux Foundation | OWASP Foundation |
| Primary Purpose | Centered on license compliance and distribution management | Optimized for security analysis and vulnerability management |
| Data Model | Capable of complex, detailed documentation | Lightweight, easy to integrate with automation tools |
| Representation Formats | Tag/Value, JSON, YAML, RDF | JSON, XML, Protobuf |

### B. SLSA (Salsa): A Software Supply Chain Security Guideline

**Definition**: A supply chain security framework proposed by Google that defines four levels to ensure the integrity of the build process.

**Key Requirements**:
- **Source**: Managing code change history and requiring two-person review.
- **Build**: Building in an isolated environment and generating build provenance.
- **Common**: Continuous security audits and vulnerability scanning.

## III. Advanced Topics & Comparison

### Stage-by-Stage Response Strategy for Strengthening Supply Chain Security

| Stage | Response Strategy | Key Technologies / Tools |
|:---:|----------|-----------------|
| Development | Vetting and selecting open-source libraries | SCA (BlackDuck, Snyk), allow-list management |
| Build | Proving the integrity of the build process, issuing an SBOM | Sigstore (digital signatures), Syft/Grype |
| Deployment | Verifying deployment images, using only approved images | Admission Controller, image signature verification |
| Operation | Runtime vulnerability monitoring and emergency patching | VEX (Vulnerability Exploitability eXchange) integration |

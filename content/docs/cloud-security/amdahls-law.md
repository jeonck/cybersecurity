---
weight: 3130
title: "Amdahl's Law"
description: "An architectural principle stating that the maximum speedup achievable through parallel processing is limited by the proportion of a task that must run sequentially."
icon: "speed"
date: "2026-08-18"
lastmod: "2026-08-18"
draft: false
---

## I. Overview

```mermaid
%%{init: { 'theme': 'base', 'themeVariables': { 'edgeLabelBackground': '#fff' }}}%%
flowchart LR
    A["Work that depends\non sequential execution"] -- "Deriving the limit of\nspeedup under parallel processing" --> B["Overall system\nspeedup"]
    style A fill:#f9f9f9,stroke:#333,stroke-width:3px
    style B fill:#e1f5fe,stroke:#01579b,stroke-width:3px
```

**Definition**: A principle stating that the maximum speedup achievable by parallelizing a given task is limited by the proportion of that task which must inevitably run sequentially.

**Features**:  
( **Bottleneck of Sequential Processing** ) No matter how many processors are added, the portion of a system that must run sequentially (serial) gains no benefit from parallel processing.  
( **Upper Bound on Speedup** ) The higher the proportion of work that cannot participate in parallel processing, the more the overall system speedup diminishes.  
( **Importance of Architectural Design** ) Implies that designing an architecture favorable to parallel processing (MSA, distributed systems) is the key to scaling performance.  
( **Proposed by Gene Amdahl** ) Proposed in 1967 by Gene Amdahl, this theory remains the foundation for predicting parallel computing performance.

## II. Mechanism & Components

### A. Amdahl's Law Formula

`Speedup(S) = 1 / ((1 - P) + P/N)`

- `S`: The maximum overall system speedup
- `P`: The proportion of the total task that can be parallelized (proportion of parallelizable work)
- `N`: The number of available processors
- `(1-P)`: The proportion of the total task that must run sequentially (proportion of serial work)

### B. Speedup Curve as the Number of Processors Increases

```mermaid
graph LR
    N["Number of processors (N)"] --> Speedup["Overall speedup (S)"]

    subgraph AmdahlCurve["Amdahl's Law Curve"]
        direction LR
        P1["P=0.5 (50% parallelizable)"] --> Curve1["S curve - rises fast early, flattens later"]
        P2["P=0.9 (90% parallelizable)"] --> Curve2["S curve - rises slowly, then flattens"]
        P3["P=1.0 (100% parallelizable)"] --> Curve3["Ideal linear increase (S=N)"]
    end

    style Curve1 fill:#e1f5fe,stroke:#01579b
    style Curve2 fill:#fff3e0,stroke:#ff9800
    style Curve3 fill:#f1f8e9,stroke:#7cb342
```

## III. Advanced Topics & Comparison

### Applications of Amdahl's Law in Parallel Computing Environments

| Application Area | Details | Security and Performance Implications |
|:---:|----------|------------------|
| **Large-Scale Data Processing** | Big data analytics, machine learning model training, etc. | Optimizing sequential logic (preprocessing, result aggregation) is critical |
| **Distributed Systems** | Inter-service communication within an MSA environment | Network latency acts as sequential processing time |
| **Parallel Attack/Defense** | Distributed DDoS attacks, multi-threaded vulnerability scanning | Attack/defense efficiency does not scale proportionally with parallel resources |

### Strategies for Overcoming the Limits of Amdahl's Law

- **Maximizing the Parallelizable Portion**: Design the architecture to minimize the proportion of sequential work (1-P) in the overall system
- **Efficient Communication Channels**: Maximize the value of P (proportion parallelizable) by reducing inter-node communication overhead (e.g. gRPC, RDMA)
- **Finer-Grained Parallel Units**: Increase parallel processing efficiency by dividing the overall task into small, independent units rather than large ones

> **Key point**: Amdahl's Law dispels the illusion that parallel computing is a cure-all, underscores the importance of **architectural design**, and shows that continually managing a system's **sequential bottlenecks** is the key to performance optimization.

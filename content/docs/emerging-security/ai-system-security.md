---
weight: 11010
title: "AI System Security"
description: "A security framework and set of techniques for protecting the confidentiality, integrity, and availability of AI models and the systems built around them."
icon: "security"
date: "2026-08-18"
lastmod: "2026-08-18"
draft: false
---

## I. Overview

```mermaid
%%{init: { 'theme': 'base', 'themeVariables': { 'edgeLabelBackground': '#fff' }}}%%
flowchart LR
    A["Traditional IT systems\nStructured data, predictable"] -- "Adoption of AI models\nUnstructured data, probabilistic output" --> B["New attack vectors\nAdversarial attacks, data poisoning"]
    style A fill:#f9f9f9,stroke:#333,stroke-width:3px
    style B fill:#e1f5fe,stroke:#01579b,stroke-width:3px
```

**Definition**: A security framework and set of techniques for ensuring the confidentiality, integrity, and availability ( **CIA** ) of artificial intelligence ( **AI** ) models and the systems built around them.

**Features**:  
( **New attack vectors** ) AI-specific threats — such as adversarial attacks and data poisoning — exist and are difficult to defend against with conventional IT security alone.  
( **Data privacy** ) Strong protective measures are required against the leakage and re-identification of sensitive training data.  
( **Model integrity** ) Attacks that damage the integrity of the AI model itself or induce bias, causing malfunctions, must be prevented.  
( **Complex systems** ) Security considerations arise across the entire AI lifecycle: data collection, preprocessing, model training, deployment, and inference.

## II. Mechanism & Components

### AI System Attack Surface

```mermaid
graph TD
    subgraph A["AI Workload"]
        AI1["Data collection /\npreprocessing"] --> AI2["Model training /\ntuning"]
        AI2 --> AI3["Model deployment /\nserving"]
        AI3 --> AI4["Inference / prediction\nAI application"]
    end
    subgraph B["AI Infrastructure"]
        BI1["Data storage\nDB, data lake"]
        BI2["Training environment\nGPU, ML platform"]
        BI3["API endpoints"]
    end
    subgraph C["AI Lifecycle\nMLOps"]
        CI1["Data pipeline\nMLOps"]
        CI2["Model registry"]
    end

    A & B & C -->|"Attack vector"| Threats["Key threats:\nAdversarial Attacks, Data Poisoning,\nModel Inversion, Privacy Leakage"]
```

### Key AI-Specific Attack Types

| Attack Type | Description | Threat |
|:---:|----------|----------|
| **Adversarial Attacks** | Adds subtle noise to input data to cause the model to malfunction | - **Evasion**: Causes a trained model's normal classification to fail (e.g., evading malware detection) <br/>- **Perturbation**: Distorts classification results through minute changes (e.g., inducing image-classification errors) |
| **Data Poisoning** | Injects malicious data into the training data to degrade the model's performance or induce a specific outcome | - **Backdoor creation**: Induces an intended malfunction for a specific input <br/>- **Performance degradation**: Reduces the model's overall accuracy |
| **Model Inversion / Extraction** | Infers or steals the structure or training data of a trained model | - **Training-data privacy breach**: Risk of leaking sensitive personal information <br/>- **Model theft**: Leakage of proprietary technology or use in further attacks |
| **Privacy Violation** | Leakage of personal information from the data a model was trained on | Includes **Membership Inference Attacks**, among others |

## III. Advanced Topics & Comparison

### Securing the AI Lifecycle

- **Data security**: Verify the integrity of training data and apply privacy-protection measures such as **pseudonymization** and **differential privacy**.
- **Model security**: Apply adversarial-defense techniques ( **Adversarial Training** ) and model-integrity verification ( **Model Integrity Check** ).
- **API security**: Enforce access control, **rate limiting**, and input/output validation ( **Input/Output Validation** ) on AI service APIs such as LLMs.
- **Continuous monitoring**: Monitor AI system operational logs and model performance for signs of anomalies.

### New Paradigms in AI Security

- **AI for Security**: Use AI technology to strengthen security threat detection and response capabilities ( **UEBA**, **Anomaly Detection** ).
- **Security for AI**: Develop technology to analyze and defend against vulnerabilities in AI systems themselves.

> **Key point**: AI system security demands an approach fundamentally different from traditional IT security, and **multi-layered defense** spanning data, models, and infrastructure is essential.

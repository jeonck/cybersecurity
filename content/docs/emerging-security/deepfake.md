---
weight: 11020
title: "Deepfake"
description: "AI-generated synthetic media, most often produced with GANs, that convincingly fabricates a person's face or voice and creates new risks for disinformation and identity fraud."
icon: "face_retouching_off"
date: "2026-08-18"
lastmod: "2026-08-18"
draft: false
---

## I. Overview

```mermaid
%%{init: { 'theme': 'base', 'themeVariables': { 'edgeLabelBackground': '#fff' }}}%%
flowchart LR
    A["Source media\nOriginal video / image"] -- "GAN-based generative model" --> B["Synthesized content\nDeepfake output"]
    style A fill:#f9f9f9,stroke:#333,stroke-width:3px
    style B fill:#e1f5fe,stroke:#01579b,stroke-width:3px
```

**Definition**: Realistic fake video or audio content that uses deep learning — particularly **GANs** (Generative Adversarial Networks) — to synthesize or edit a specific person's face or voice.

**Features**:  
( **Realistic manipulation** ) Achieves a level of realism that is difficult to distinguish from genuine content, beyond what conventional image or video editing can produce.  
( **Malicious use** ) Increasingly used to spread fake news, commit defamation, carry out financial fraud ( **voice phishing** ), and fuel political disinformation, raising the risk of social disruption.  
( **Identity theft** ) A specific person's voice or face can be misappropriated without authorization and abused in impersonation crimes.

## II. Mechanism & Components

### GAN (Generative Adversarial Network)-Based Generative Model

```mermaid
sequenceDiagram
    participant G as Generator
    participant D as Discriminator
    participant T as Training Data

    Note over G,D: The two networks learn by competing with each other
    G->>D: Generates a fake image (from initial random noise)
    D->>T: Learns from real images
    D->>G: Feeds back the real/fake judgment
    G->>G: Improves the generative model to fool the discriminator (gradient descent)
    Note over G,D: Through repeated training, the generator produces increasingly realistic fake images,<br/>while the discriminator gets better at telling real from fake
```

### Deepfake Generation Process

1. **Data collection**: Gather a large volume of source data — the target person's face, expressions, voice, and so on — for training the **AI** model.
2. **Model training**: Use a **GAN** to learn the features of the source data and train a new model that synthesizes faces or voices.
3. **Content generation**: Feed inputs (a target face or voice) into the trained model to generate manipulated deepfake video or audio.
4. **Post-processing (optional)**: Edit and refine the generated content so it appears more natural.

## III. Adoption Considerations

| Risk | Mitigation |
|---|---|
| Fabricated content spread as disinformation or used in impersonation fraud | AI-based detection of visual/auditory artifacts (unnatural blinking, voice-alteration traces), **watermarking** at creation time, blockchain-based digital provenance |
| Voice/video impersonation used for social engineering (voice phishing, executive-impersonation fraud) | Out-of-band verification for high-value requests, not caller/sender identity alone |
| Unauthorized use of a person's likeness or voice, and slow platform takedown | Stronger anti-abuse legislation, mandatory platform detection and takedown obligations, public awareness education |

The organizational fix for deepfake-enabled fraud looks a lot like the fix for email-based CEO fraud a decade ago: a mandatory out-of-band verification step for any high-value request, regardless of how convincing the voice or video sounds. Detection technology will keep losing an arms race against generation technology, so the process control — not detection accuracy — should carry the weight of the defense.

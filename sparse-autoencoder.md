---
title: Sparse Autoencoders
description: Learn about Sparse Autoencoders (SAEs) and the models supported on Neuronpedia
---

# Sparse Autoencoders

## What are Sparse Autoencoders?

Sparse Autoencoders (SAEs) are a method to extract interpretable features from neural networks. They help researchers understand what models "know" by decomposing model activations into human-interpretable concepts.

[Learn more about SAEs from Anthropic's research](https://transformer-circuits.pub/2023/monosemantic-features)

## SAE Naming Convention

Every Sparse Autoencoder on Neuronpedia has a unique identifier in the format:

`MODEL`@`LAYER`-`DESCRIPTION`-`AUTHOR`

### Example

The `GPT2-SMALL@9-RES-JB` SAE refers to:
- **Model**: GPT2-Small
- **Layer**: 9
- **Hook**: Residual Stream
- **Author**: Joseph Bloom

This SAE is located at [`https://neuronpedia.org/gpt2-small/9-res-jb`](https://neuronpedia.org/gpt2-small/9-res-jb).

![Screenshot of https://neuronpedia.org/gpt2-small/9-res-jb showing a UMAP and dots representing features.](https://github.com/AaronBergman/docs/blob/main/images/sae-example.png)

## SAE Organization: Sets & Releases

Since researchers usually release SAEs for multiple layers at once, Neuronpedia organizes SAEs into two hierarchical levels:

### SAE Set
One or more SAEs that analyze the same hook and use the same method, across different layers.

**Example:** [RES-JB](https://www.neuronpedia.org/gpt2-small/res-jb) is an SAE Set with 12 SAEs based on the residual stream of GPT2-Small's 12 layers.

### SAE Release
One or more SAE Sets, typically corresponding to a research paper and containing all SAEs trained/analyzed in it.

**Example:** [P70D-SM](https://www.neuronpedia.org/p70d-sm) is an SAE Release containing three SAE Sets:
- Attention Out ([ATT-SM](https://www.neuronpedia.org/pythia-70m-deduped/att-sm))
- MLP Post ([MLP-SM](https://www.neuronpedia.org/pythia-70m-deduped/mlp-sm))
- Residuals ([RES-SM](https://www.neuronpedia.org/pythia-70m-deduped/res-sm))

![Diagram that shows SAE Release as the largest rectangle, with two SAE Sets in that rectangle, and 3 SAEs in each of the 2 SAE Sets.](https://github.com/AaronBergman/docs/blob/main/images/sae-groupings.png)

## Supported Models & SAE Releases

Neuronpedia supports a growing collection of models and SAE releases. Here are some notable examples:

### GPT2-Small
- **RES-JB**: Residual stream SAEs by Joseph Bloom
- **MLP-OAI**: MLP layer SAEs from OpenAI's release
- Multiple other SAE sets available

### Gemma Scope (Gemma 2)
Google DeepMind's Gemma Scope SAEs provide comprehensive coverage of Gemma 2 models:

- **gemma-2-2b** and **gemma-2-2b-it** (instruction-tuned variant)
  - Multiple widths available, including the gemmascope-res-16k SAEs (all layers)
  - First 1M width SAE: `gemma-2-2b - 12-gemmascope-res-1m`
- **gemma-2-9b**
  - Supports auto-interpretation, scoring, and all Neuronpedia features

[Explore Gemma Scope SAEs](https://www.neuronpedia.org/gemma-scope)

### Llama Scope (Llama 3.1-8B)
Llama Scope SAEs by He et al. (2024) provide 32k width coverage:

- **Residual Stream (LXR-8x)**: All layers available
- **MLP (LXM-8x)**: All layers available
- Full support for dashboards, autointerp, search, steering, and activation testing

[Explore Llama Scope SAEs](https://www.neuronpedia.org/llama-scope)

### DeepSeek R1 Distill
SAEs for reasoning models:

- **deepseek-r1-distill-llama-8b**
- Using `llamascope-slimpj-res-32k` (layer 15)
- Trained by OpenMOSS

### Pythia Models
- Multiple SAE releases for Pythia-70M-deduped
- Attention, MLP, and Residual stream coverage

### Qwen3 (4B)
- Support for Qwen3 4B model with SAEs

### CrossCoders
Advanced interpretability methods beyond traditional SAEs:

- **Dumas/Minder CrossCoders**: Uploaded via Neuronpedia APIs
- Example: [Date/days/time feature](https://neuronpedia.org) with autointerp and steering support

### Multi TopK SAEs
New SAE architecture with improved performance:

- **Llama 3.1-8B**: `eleuther_gp-mlp-262k`
- Multi TopK architecture for better feature extraction

## Beyond SAEs

Neuronpedia has expanded beyond Sparse Autoencoders to support all forms of mechanistic interpretability research:

- **Probes**: Linear probes for specific concepts
- **Concepts**: Custom interpretability concepts
- **Transcoders**: Cross-model feature translation
- **Circuit Tracing**: Attribution graphs and model reasoning analysis
- **Custom Vectors**: Upload and analyze your own steering vectors

You can upload your own dashboards and vectors using the [Neuronpedia Python Library](python-library) - see the Upload section for details.

## Finding SAEs

To explore available SAEs:

1. **Browse by model**: Visit [neuronpedia.org](https://neuronpedia.org) and select a model
2. **Search features**: Use the search functionality to find features across SAE sets
3. **API access**: Use the [REST API](api) or [Python Library](python-library) for programmatic access

## Learn More

- [Anthropic's Monosemanticity Paper](https://transformer-circuits.pub/2023/monosemantic-features)
- [Gemma Scope Blog Post](https://neuronpedia.org/blog)
- [Neuronpedia Python Library](python-library)
- [Upload Your Own SAEs](upload-saes)

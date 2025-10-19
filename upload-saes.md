---
title: Upload Your SAEs
description: Upload custom SAEs, vectors, and dashboards to Neuronpedia
---

# Upload Your SAEs

**Updated November 2024**: Uploading to Neuronpedia is now easy with the Python Library!

## Quick Start with Python Library

Upload custom vectors and dashboards in just a few lines of code:

### Upload a Custom Vector

```python
from neuronpedia import NeuronpediaClient

client = NeuronpediaClient(api_key="your-api-key")

# Upload your vector
vector_id = client.upload_vector(
    vector=[0.23, -0.45, 0.12, ...],  # Your vector values
    name="My Custom Vector",
    description="Detects X in model Y"
)

# Your vector is now live with full Neuronpedia support!
```

### Upload a Full Dashboard

Upload a complete feature dashboard with all Neuronpedia infrastructure in ~5 lines:

```python
from neuronpedia import upload_dashboard

dashboard_id = upload_dashboard(
    model="your-model",
    vector=[0.1, 0.2, 0.3, ...],
    name="My Custom Feature",
    description="A feature that detects...",
    metadata={
        "sparsity": 0.001,
        "layer": 6
    }
)
```

### What You Get Automatically

Uploaded features automatically get:
- ✅ **Activation testing** with custom text
- ✅ **Auto-interpretation** using GPT-4 or EleutherAI
- ✅ **Explanation scoring** with multiple methods
- ✅ **Steering support** - use your feature to control outputs
- ✅ **Lists and sharing** - organize and collaborate
- ✅ **Embedding** - embed in websites and documentation
- ✅ **All Neuronpedia tools** - search, attribution graphs, etc.

## Upload Entire SAE Sets

Upload all features from your SAE:

```python
from neuronpedia import NeuronpediaClient

client = NeuronpediaClient(api_key="your-api-key")

# Upload all features from your SAE
for idx, vector in enumerate(sae_vectors):
    client.upload_feature(
        model="your-model",
        sae_id="your-sae-32k",
        layer=6,
        index=idx,
        vector=vector,
        metadata={
            "sparsity": sparsity_values[idx],
            "frequency": frequency_values[idx],
            "max_activation": max_acts[idx]
        }
    )

    if idx % 100 == 0:
        print(f"Uploaded {idx} features...")
```

## Supported Upload Types

### 1. SAE Features

Standard SAE features from your trained autoencoders:

```python
client.upload_feature(
    model="llama-3-8b",
    sae_id="my-sae-16k",
    layer=12,
    index=1234,
    vector=feature_vector
)
```

### 2. CrossCoders

Upload CrossCoder or Transcoder features:

```python
from neuronpedia import upload_crosscoder_features

upload_crosscoder_features(
    model="gemma-2b",
    crosscoder_id="my-crosscoder",
    features=crosscoder_features,
    layer=6
)
```

**Example**: Dumas/Minder CrossCoders were uploaded using this method.

### 3. Steering Vectors

Upload steering vectors from research papers or your own experiments:

```python
vector_id = client.upload_vector(
    vector=refusal_vector,
    name="Refusal Steering (Arditi et al.)",
    description="Reduces model refusal behavior",
    tags=["steering", "safety"]
)
```

### 4. Probes and Concepts

Upload linear probes or concept vectors:

```python
client.upload_probe(
    model="gpt2-small",
    probe_vector=probe_weights,
    name="Truthfulness Probe",
    concept="truthfulness"
)
```

## Batch Upload

For uploading many features efficiently:

```python
# Prepare batch
features_batch = [
    {
        "model": "gpt2-small",
        "sae_id": "my-sae",
        "index": i,
        "vector": vectors[i],
        "metadata": metadata[i]
    }
    for i in range(1000)
]

# Upload in batches of 100
client.batch_upload_features(features_batch, batch_size=100)
```

## Authentication

Get your API key:

1. Visit [neuronpedia.org/settings](https://neuronpedia.org/settings)
2. Log in (create account if needed)
3. Generate an API key
4. Use it in your code:

```python
client = NeuronpediaClient(api_key="your-api-key")
```

Or set as environment variable:
```bash
export NEURONPEDIA_API_KEY="your-api-key"
```

## Upload Via Form (Alternative)

Prefer not to code? Fill out our upload form and we'll handle it:

[Upload Form](https://docs.google.com/forms/d/e/1FAIpQLSdBrFZAWXww1hnyVpGaVvxNCbhTO2nhMkdJHIG0T9-W7gcpUw/viewform) (< 5 minutes)

We'll get back to you within 72 hours.

## Data Format

### Vector Format

Vectors should be:
- Python list or NumPy array
- Float values
- Same dimension as model's residual stream

```python
# Good
vector = [0.1, 0.2, 0.3, ...]  # List
vector = np.array([0.1, 0.2, 0.3, ...])  # NumPy

# Supported dimensions
# GPT2-Small: 768
# Gemma-2-2B: 2048
# Llama-3-8B: 4096
```

### Metadata (Optional but Recommended)

Provide metadata for better discoverability:

```python
metadata = {
    "sparsity": 0.001,  # Feature sparsity
    "frequency": 0.05,  # Activation frequency
    "layer": 6,  # Which layer
    "max_activation": 12.3,  # Max activation value
    "training_tokens": 1000000,  # Tokens used for training
    "l0": 50,  # L0 sparsity
    "dead": False  # Is this a dead feature?
}
```

## Privacy & Visibility

### Public vs Private

- **Public** (default): Anyone can view and use your features
- **Private**: Only you can access (requires paid plan)

Set visibility during upload:

```python
client.upload_feature(
    model="my-model",
    vector=vector,
    visibility="private"  # or "public"
)
```

### Licensing

By default, uploads are licensed under CC-BY 4.0. You can specify a different license:

```python
client.upload_feature(
    model="my-model",
    vector=vector,
    license="MIT"  # or "Apache-2.0", "CC0", etc.
)
```

## Rate Limits

Upload rate limits:

- **Free tier**: 1000 features/day
- **Research tier**: 10,000 features/day
- **Bulk uploads**: Contact us for higher limits

Email [support@neuronpedia.org](mailto:support@neuronpedia.org) if you need to upload more.

## Examples

### Example 1: Upload GPT2-Small SAE

```python
import numpy as np
from neuronpedia import NeuronpediaClient

# Load your SAE weights
sae_weights = np.load("my_sae_weights.npy")

client = NeuronpediaClient(api_key="your-api-key")

# Upload all features
for idx in range(sae_weights.shape[0]):
    client.upload_feature(
        model="gpt2-small",
        sae_id="my-experimental-sae",
        layer=9,
        index=idx,
        vector=sae_weights[idx].tolist()
    )
```

### Example 2: Upload Steering Vector from Paper

```python
from neuronpedia import NeuronpediaClient

client = NeuronpediaClient(api_key="your-api-key")

# Vector from Arditi et al. refusal steering paper
refusal_vector = [...]  # Your vector values

vector_id = client.upload_vector(
    vector=refusal_vector,
    name="Refusal Steering",
    description="Steering vector to reduce refusal (Arditi et al.)",
    tags=["steering", "safety", "refusal"],
    paper_url="https://arxiv.org/abs/..."
)

# Now you can steer with it!
result = client.steer(
    model="gemma-2b",
    vector_id=vector_id,
    strength=-5,
    prompt="How do I..."
)
```

### Example 3: Upload with Auto-Interpretation

```python
# Upload and automatically generate explanation
dashboard_id = client.upload_dashboard(
    model="gpt2-small",
    vector=[0.1, 0.2, ...],
    name="Possible measurement feature",
    auto_interpret=True,  # Generate explanation automatically
    interpretation_method="eleuther"
)

# Check the explanation
feature = client.get_feature(dashboard_id)
print(feature.explanation)
```

## Troubleshooting

### Common Issues

**"Invalid vector dimension"**
- Ensure vector length matches model dimension
- GPT2-Small: 768, Gemma-2B: 2048, etc.

**"Rate limit exceeded"**
- Reduce upload speed or batch size
- Contact us for higher limits

**"Authentication failed"**
- Check API key is correct
- Ensure key has upload permissions

### Getting Help

- **Python Library Docs**: [Full documentation](python-library)
- **API Sandbox**: [neuronpedia.org/api-doc](https://neuronpedia.org/api-doc)
- **Slack**: [#neuronpedia channel](https://join.slack.com/t/opensourcemechanistic/shared_invite/zt-375zalm04-GFd5tdBU1yLKlu_T_JSqZQ)
- **Email**: [support@neuronpedia.org](mailto:support@neuronpedia.org)

## Learn More

- [Python Library](python-library) - Complete library documentation
- [API Documentation](api) - REST API reference
- [Features](features) - Understanding feature dashboards
- [Steering](steering) - Using uploaded vectors for steering
- [Auto-Interpretation](auto-interp) - Generating explanations

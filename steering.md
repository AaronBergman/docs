---
title: Steering
description: Control model outputs using SAE features or custom steering vectors
---

# Steering

Neuronpedia supports steering model outputs by increasing or decreasing the strength of SAE features or custom vectors during generation.

You can think of this as similar to Anthropic's "Golden Gate Claude" demonstration - but you can use any feature or custom vector, not just features about the Golden Gate Bridge.

## Supported Models

Neuronpedia supports steering for multiple models including:
- **Gemma-2B** and **Gemma-2B-IT** (instruction-tuned)
- **Gemma-2-9B**
- **GPT2-Small**
- **Llama 3.1-8B** (via Llama Scope SAEs)
- More models being added regularly

Visit [`https://www.neuronpedia.org/steer`](https://www.neuronpedia.org/steer) to try steering.

## Steering with SAE Features

To steer using an SAE feature:

1. Navigate to any feature dashboard
2. Click the "Steer" button or tab
3. Adjust the steering strength (positive or negative values)
4. Enter your prompt
5. Generate text to see how the feature influences the output

### Example: Steering GPT2-Small

Here's a Python example showing how to steer GPT2-Small with a feature about San Francisco:

```python
import json
import requests

# Prompt and model
PROMPT = "The most iconic structure on Earth is"
MODEL_ID = "gemma-2b"

# Feature about San Francisco
FEATURE = {
    "modelId": "gemma-2b",
    "layer": "6-res-jb",
    "index": 10200,
    "strength": 5
}

# Generation settings
TEMPERATURE = 0.2
N_TOKENS = 16
FREQ_PENALTY = 1.0
SEED = 16
STRENGTH_MULTIPLIER = 4

# Make the API request
url = "https://www.neuronpedia.org/api/steer"
data = {
    "prompt": PROMPT,
    "modelId": MODEL_ID,
    "features": [FEATURE],
    "temperature": TEMPERATURE,
    "n_tokens": N_TOKENS,
    "freq_penalty": FREQ_PENALTY,
    "seed": SEED,
    "strength_multiplier": STRENGTH_MULTIPLIER,
}
headers = {"Content-Type": "application/json"}

# Send request
response = requests.post(url, json=data, headers=headers)
json_response = response.json()
formatted_response = json.dumps(json_response, indent=4)
print(formatted_response)
```

## Custom Steering Vectors

**New in November 2024:** You can now upload and use your own steering vectors, not just SAE features!

### Why Use Custom Vectors?

Custom steering vectors allow you to:
- Steer with vectors that aren't part of an SAE
- Use vectors from research papers (e.g., refusal steering from Arditi et al.)
- Test your own trained steering vectors
- Experiment with custom interventions

### How to Upload Custom Vectors

1. **Click "+ Add Vector"** on the steering interface
2. **Paste your steering vector** (as a JSON array or comma-separated values)
3. **Test immediately** - your vector is ready to use right away
4. **Save to your library** - vectors are automatically saved to "My Vectors" for reuse

### Managing Your Vectors

After logging in, click **"My Vectors"** in the navbar to:
- View all your uploaded vectors
- Edit vector names and descriptions
- Test vectors with custom activation text
- Delete vectors you no longer need

### Example: Refusal Steering

You can upload refusal steering vectors from research papers to reduce or increase model refusal behavior:

```python
from neuronpedia import upload_vector, steer_with_vector

# Upload a custom refusal vector
vector_id = upload_vector(
    name="Refusal Steering",
    vector=[0.23, -0.45, 0.12, ...],  # Your vector values
    description="Refusal steering from Arditi et al."
)

# Use it for steering
result = steer_with_vector(
    model="gemma-2b",
    vector_id=vector_id,
    prompt="How do I...",
    strength=-5  # Negative to reduce refusal
)
```

### Custom Activation Testing

Like SAE features, custom vectors support:
- **Custom text testing** - Test how your vector activates on specific text
- **Shareable results** - Generate links to share your activation tests
- **Embedding** - Embed vector dashboards in other sites

## Using the Python Library

The [Neuronpedia Python Library](python-library) makes steering even easier:

```python
from neuronpedia import NeuronpediaClient

client = NeuronpediaClient()

# Steer with an SAE feature
result = client.steer(
    model="gemma-2b",
    feature_id="6-res-jb:10200",
    strength=5,
    prompt="The most iconic structure on Earth is"
)

# Or upload and steer with a custom vector in just 3 lines
vector_id = client.upload_vector([0.1, 0.2, ...], name="My Vector")
result = client.steer(model="gemma-2b", vector_id=vector_id, strength=5)
```

See the [Python Library documentation](python-library) for more examples.

## Rate Limits

There is an hourly rate limit of **100 steers per user** to ensure fair usage.

## API Documentation

For complete API details, see the [API Docs](https://neuronpedia.org/api-doc) or the [API page](api).

## Learn More

- [Neuronpedia Python Library](python-library) - Easiest way to steer programmatically
- [Upload Your Own Vectors](upload-saes) - More details on uploading custom vectors
- [API Documentation](api) - Full API reference
- [Anthropic's Golden Gate Claude](https://www.anthropic.com/news/golden-gate-claude) - Inspiration for steering

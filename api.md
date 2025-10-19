---
title: API & Exports
description: Access Neuronpedia data programmatically via REST API or data exports
---

# API & Exports

## Python Library (Recommended)

**The easiest way to interact with Neuronpedia programmatically is the [Python Library](python-library).**

The official Neuronpedia Python Library provides:
- Clean, intuitive API for all Neuronpedia features
- Complete coverage of endpoints
- Automatic authentication handling
- Extensive documentation and examples

```bash
pip install neuronpedia
```

See the [Python Library documentation](python-library) for details.

## REST API

Neuronpedia has a public REST API to access all data, including features, explanations, activations, steering, and more.

### API Documentation

Interactive API documentation and sandbox: [https://neuronpedia.org/api-doc](https://neuronpedia.org/api-doc)

You can test all endpoints directly in your browser.

### Key Endpoints

#### Features

Get feature data:
```
GET https://neuronpedia.org/api/feature/{model}/{sae_id}/{index}
```

Example: [https://neuronpedia.org/api/feature/gpt2-small/6-res_scefr-ajt/650](https://neuronpedia.org/api/feature/gpt2-small/6-res_scefr-ajt/650)

#### Search

Search features by activation:
```
POST https://neuronpedia.org/api/search
```

#### Steering

Steer model outputs:
```
POST https://neuronpedia.org/api/steer
```

See the [Steering documentation](steering) for example code.

#### Auto-Interpretation

Generate explanations:
```
POST https://neuronpedia.org/api/explanation-type/eleuther_acts_top20
```

Score explanations:
```
POST https://neuronpedia.org/api/score-type/eleuther_embedding
POST https://neuronpedia.org/api/score-type/eleuther_fuzz
POST https://neuronpedia.org/api/score-type/eleuther_recall
```

See the [Auto-Interpretation documentation](auto-interp) for details.

#### Upload

Upload custom vectors and dashboards:
```
POST https://neuronpedia.org/api/upload/vector
POST https://neuronpedia.org/api/upload/dashboard
```

### Authentication

For write operations (uploading, creating lists, etc.), include your API key:

```bash
curl -H "Authorization: Bearer YOUR_API_KEY" \
  https://neuronpedia.org/api/upload/vector
```

Get your API key from [neuronpedia.org/settings](https://neuronpedia.org/settings) (requires login).

### Rate Limits

- **Steering**: 100 requests per hour per user
- **Search**: Unlimited for most operations
- **Upload**: Contact us for bulk upload needs

## Data Exports

For your convenience (and to avoid hammering our server), we provide full data exports.

### Latest Exports (v1)

Download 4+ terabytes of interpretability data:

[https://neuronpedia-datasets.s3.us-east-1.amazonaws.com/index.html?prefix=v1/](https://neuronpedia-datasets.s3.us-east-1.amazonaws.com/index.html?prefix=v1/)

Includes:
- **11 models**
- **60+ million latents/features/concepts**
- **50+ million explanations**
- **3+ billion activations**

### What's in the Exports?

Each export includes:
- Feature vectors and metadata
- Top activations with highlighted tokens
- Auto-generated explanations
- Scores and evaluations
- Logits and statistics
- Related features and neurons

### Export Format

Data is provided in JSON format, organized by:
- Model (e.g., `gpt2-small`, `gemma-2-2b`)
- SAE ID (e.g., `6-res-jb`)
- Feature index

### Older Exports

Legacy exports are still available:

[https://neuronpedia-exports.s3.amazonaws.com/index.html](https://neuronpedia-exports.s3.amazonaws.com/index.html)

## Custom Exports

Need specific data not in the exports? [Email us](mailto:support@neuronpedia.org) - we can usually provide custom exports within 48 hours.

## OpenAPI Schema

The API follows OpenAPI specification for easy integration with tools and frameworks.

View the schema: [https://neuronpedia.org/api/openapi.json](https://neuronpedia.org/api/openapi.json)

## Code Examples

### Python (using requests)

```python
import requests

# Get a feature
response = requests.get(
    "https://neuronpedia.org/api/feature/gpt2-small/6-res-jb/650"
)
feature_data = response.json()

# Search features
search_response = requests.post(
    "https://neuronpedia.org/api/search",
    json={
        "model": "gpt2-small",
        "sae_set": "res-jb",
        "text": "Your search text here",
        "top_k": 20
    }
)
results = search_response.json()
```

### JavaScript/TypeScript

```javascript
// Get a feature
const response = await fetch(
  'https://neuronpedia.org/api/feature/gpt2-small/6-res-jb/650'
);
const featureData = await response.json();

// Search features
const searchResponse = await fetch(
  'https://neuronpedia.org/api/search',
  {
    method: 'POST',
    headers: { 'Content-Type': 'application/json' },
    body: JSON.stringify({
      model: 'gpt2-small',
      sae_set: 'res-jb',
      text: 'Your search text here',
      top_k: 20
    })
  }
);
const results = await searchResponse.json();
```

### cURL

```bash
# Get a feature
curl https://neuronpedia.org/api/feature/gpt2-small/6-res-jb/650

# Search features
curl -X POST https://neuronpedia.org/api/search \
  -H "Content-Type: application/json" \
  -d '{
    "model": "gpt2-small",
    "sae_set": "res-jb",
    "text": "Your search text here",
    "top_k": 20
  }'
```

## Getting Help

- **API Sandbox**: [neuronpedia.org/api-doc](https://neuronpedia.org/api-doc)
- **Python Library**: [Complete documentation](python-library)
- **Slack**: [Open Source Mechanistic Interpretability workspace](https://join.slack.com/t/opensourcemechanistic/shared_invite/zt-375zalm04-GFd5tdBU1yLKlu_T_JSqZQ)
- **Email**: [support@neuronpedia.org](mailto:support@neuronpedia.org)

## Learn More

- [Python Library](python-library) - Easiest way to use the API
- [Steering](steering) - API examples for steering
- [Auto-Interpretation](auto-interp) - Explanation and scoring endpoints
- [Upload SAEs](upload-saes) - Upload your own features

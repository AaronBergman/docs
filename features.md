---
title: Features
description: Explore individual SAE features with dashboards, explanations, and interactive tools
slug: /features
---

# SAE Features

## What's a Feature?

Sparse Autoencoders identify many **features** in a model, each representing a concept or pattern that the model has learned. A **feature dashboard** on Neuronpedia is an interactive way to examine a feature, showing:

- Statistics and metadata
- Positive and negative logits
- Correlated neurons
- Top activations
- Auto-generated explanations
- Custom activation testing

## Feature URLs

Each feature has a unique ID: `[MODEL_ID]@[SAE_ID]:[FEATURE_INDEX]`

Features are located at: `https://neuronpedia.org/[MODEL_ID]/[SAE_ID]/[FEATURE_INDEX]`

### Example Feature

Let's explore feature 650 from GPT2-Small, layer 6, SAE Set `RES_SCEFR-AJT`:

[`https://neuronpedia.org/gpt2-small/6-res_scefr-ajt/650`](https://neuronpedia.org/gpt2-small/6-res_scefr-ajt/650)

![Screenshot of a feature dashboard at https://www.neuronpedia.org/gpt2-small/6-res_scefr-ajt/650](img/feature-dashboard.png)

## Feature Dashboard Components

### Basic Statistics

Every feature dashboard shows:
- **Activation frequency** - How often the feature activates
- **Max activation** - Strongest activation value seen
- **Feature sparsity** - How selective the feature is
- Hover over (?) icons for detailed explanations

### Logits Analysis

View the top positive and negative logits to understand:
- What tokens the feature promotes
- What tokens the feature suppresses
- How the feature influences model outputs

### Top Activations

See real examples of text where the feature activated strongly:
- Highlighted tokens show activation strength
- Click to explore activation patterns
- Sort and filter by activation values

## Auto-Interpretation & Explanations

**Updated in November 2024** with EleutherAI integration!

### What is Auto-Interpretation?

Auto-interpretation uses AI models (GPT-4, Claude, or specialized explainers) to generate human-readable explanations of what a feature detects.

![Screenshot of a feature explanation at https://www.neuronpedia.org/gpt2-small/6-res_scefr-ajt/650](img/feature-explanation.png)

### Multiple Explanation Methods

Generate explanations using different approaches:

1. **GPT-4 / GPT-3.5-Turbo** - Based on top activations
2. **EleutherAI Explainer** - Specialized interpretability model
3. **Community explanations** - Human-written descriptions

### Explanation Scoring

Explanations can be scored to evaluate quality:

- **GPT-based scoring** - Traditional scoring method
- **EleutherAI Embedding** - Semantic similarity scoring
- **EleutherAI Fuzz** - Fuzzy matching scoring
- **EleutherAI Recall** - Recall-based evaluation

Scores range from 0-100. Click any score to see scoring details:

![Screenshot of a feature score and details at https://www.neuronpedia.org/gpt2-small/6/200](img/feature-scored.png)

### How to Generate Explanations

1. Navigate to a feature dashboard
2. Click the explanation type dropdown
3. Select your preferred method (e.g., "EleutherAI Explainer")
4. Click "Generate"
5. View the explanation and optional score

You can also vote on explanations and add your own!

## Test Activations

**Updated with sharing functionality in November 2024!**

Every feature can be tested with custom text to validate theories and explore behavior.

### How to Test

1. Find the "Test Activations" section on any feature
2. Enter your custom text
3. View activation strengths on each token
4. Adjust text to explore different contexts

![Screenshot of a feature test at https://www.neuronpedia.org/gpt2-small/6-res_scefr-ajt/650](img/feature-test.png)

### Share Your Tests

**New:** Click the **"↑ Share"** button to:
- Generate a shareable link with your custom test
- Share activation results with colleagues
- Embed tests in documentation or posts
- No more screenshots needed!

See [Search documentation](search) for more details on sharing.

## Feature Lists

Organize and curate collections of interesting features:

- **Create lists** with descriptions and themes
- **Add features** from any model or SAE
- **Share lists** publicly or keep them private
- **Collaborate** with other researchers

Lists are perfect for:
- Research projects
- Teaching materials
- Documenting findings
- Comparing related features

Learn more: [Lists documentation](lists)

## Comments & Discussion

Every feature has a comment section where you can:
- Discuss interpretations
- Share insights
- Ask questions
- Collaborate with the community

## Starring Features

Bookmark interesting features by **starring** them:
- Quick access from your profile
- Personal reference library
- Track features across projects

## Advanced Features

### Cosine Similarity

Compare features to find related concepts:
- Find similar features across layers
- Discover feature clusters
- Understand feature relationships

### Steering

Use features to control model outputs:
- Increase or decrease feature strength
- See how outputs change
- Experiment with model behavior

Learn more: [Steering documentation](steering)

### Attribution Graphs

Visualize how features connect and influence each other:
- See feature relationships
- Understand circuits
- Trace model reasoning

Learn more: [Attribution Graphs documentation](attribution-graphs)

## Accessing Features Programmatically

### JSON API

Get feature data in JSON format by adding `/api/feature/` to the URL:

**Feature page**: [`https://www.neuronpedia.org/gpt2-small/6-res_scefr-ajt/650`](https://www.neuronpedia.org/gpt2-small/6-res_scefr-ajt/650)

**JSON endpoint**: [`https://www.neuronpedia.org/api/feature/gpt2-small/6-res_scefr-ajt/650`](https://www.neuronpedia.org/api/feature/gpt2-small/6-res_scefr-ajt/650)

### Python Library

Use the Neuronpedia Python Library for easy programmatic access:

```python
from neuronpedia import NeuronpediaClient

client = NeuronpediaClient()

# Get feature data
feature = client.get_feature(
    model="gpt2-small",
    sae_id="6-res_scefr-ajt",
    index=650
)

# Generate explanation
explanation = client.generate_explanation(
    feature_id=feature.id,
    method="eleuther"
)

# Test with custom text
activations = client.test_feature(
    feature_id=feature.id,
    text="Your custom text here"
)
```

Learn more: [Python Library documentation](python-library)

## Sharing Features

### OpenGraph Previews

When you share a feature link on Slack, Twitter, or other platforms, a preview image is automatically generated:

![Screenshot of the OpenGraph image preview for https://www.neuronpedia.org/gpt2-small/6-res_scefr-ajt/650](img/feature-slack.png)

### Embedding Features

Embed feature dashboards in:
- Blog posts
- Research papers
- Documentation sites
- LessWrong posts (native support)

Learn more: [Embedding documentation](embed-iframe)

## Upload Your Own Features

**New in November 2024:** Upload custom dashboards with the Python Library!

You can now upload:
- Custom vectors
- Features from your own SAEs
- Probes and concepts
- Any interpretability artifacts

Uploaded features automatically get:
- Activation testing
- Auto-interpretation
- Scoring
- Steering support
- Lists and sharing
- All Neuronpedia infrastructure

Upload in just 5 lines of code:

```python
from neuronpedia import upload_dashboard

dashboard_id = upload_dashboard(
    model="your-model",
    vector=[0.1, 0.2, 0.3, ...],
    name="My Custom Feature"
)
```

Learn more: [Upload documentation](upload-saes) and [Python Library](python-library)

## Learn More

- [Search](search) - Find features by activation or explanation
- [Steering](steering) - Control model outputs with features
- [Lists](lists) - Organize and share feature collections
- [Attribution Graphs](attribution-graphs) - Visualize feature circuits
- [Auto-Interpretation](auto-interp) - Generate and score explanations
- [API Documentation](api) - Programmatic access
- [Python Library](python-library) - Easiest way to interact with features

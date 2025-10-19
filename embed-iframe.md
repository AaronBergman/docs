---
title: Embedding Features
description: Embed Neuronpedia features in websites, documentation, and posts
---

# Embedding Features

## Overview

Neuronpedia features can be embedded on your site, documentation, or third-party sites using iframes. This is perfect for:

- **Research papers** - Show feature activations inline
- **Blog posts** - Demonstrate concepts with live examples
- **Documentation** - Provide interactive feature exploration
- **LessWrong posts** - Native embedding support

## Quick Start

Every feature has an `Embed Code/Link` section with a Copy icon for quick embedding:

![Screenshot of a embed code at https://neuronpedia.org/gpt2-small/0-res-jb/14057](img/embedcode.png)

Or construct your own by adding `?embed=true` to any feature URL.

## Sharing Workflow (New!)

**Updated November 2024**: You can now easily share custom activation tests!

### Share Custom Activation Results

When testing a feature with custom text:

1. **Enter your custom text** in the activation testing section
2. **Click the "↑ Share" button**
3. **Copy the generated link** - includes your custom text and results
4. **Share or embed** - recipients see your exact test

The shared link includes:
- The feature being tested
- Your custom activation text
- Activation results
- Full interactivity for further testing

**No more screenshots needed!** Send a link and colleagues can see exactly what you're seeing.

### Example Use Case

> "Check out how this 'dogs' feature surprisingly activates on 'cats': [link with custom test]"

Recipients click the link and see your test results, then can modify the text to explore further.

See the [Search documentation](search) for more details on custom activation sharing.

## Simple Example

The following demonstrates the most basic embed for `GPT2-SMALL@0-RES-JB:14057`:

Feature URL: `https://neuronpedia.org/gpt2-small/0-res-jb/14057`

Embed URL: `https://neuronpedia.org/gpt2-small/0-res-jb/14057?embed=true`

Embed Code: `<iframe src="https://neuronpedia.org/gpt2-small/0-res-jb/14057?embed=true" title="Neuronpedia" style="height: 300px; width: 540px;"></iframe>`

And here's what the embed looks like:

<iframe src="https://neuronpedia.org/gpt2-small/0-res-jb/14057?embed=true" title="Neuronpedia" style={{border: "1px solid #ddd", borderRadius: "10px", width:"540px", height:"300px"}}></iframe>

## Customizations

### Width and Height

You can customize the width and height of the iframe by modifying the style attribute. Note that widths smaller than 640 pixels will result in stacking the dashboard vertically, and show fewer top logits (5 instead of 10).

Here's the example above, with larger width and height:

`<iframe src="https://neuronpedia.org/gpt2-small/0-res-jb/14057?embed=true&embedexplanation=true&embedplots=true" title="Neuronpedia" style={{border: "1px solid #ddd", borderRadius: "10px", width:"645px", height:"420px"}}></iframe>`

<iframe src="https://neuronpedia.org/gpt2-small/0-res-jb/14057?embed=true&embedexplanation=true&embedplots=true" title="Neuronpedia" style={{border: "1px solid #ddd", borderRadius: "10px", width:"645px", height:"420px"}}></iframe>

### Show Activation Testing

Enable or disable showing activation testing by changing query parameter `embedtest` to true or false. This is enabled by default.

#### Enabled

`<iframe src="https://neuronpedia.org/gpt2-small/0-res-jb/14057?embed=true&embedexplanation=true&embedplots=false&embedtest=true" title="Neuronpedia" style={{border: "1px solid #ddd", borderRadius: "10px", width:"480px", height:"300px"}}></iframe>`

<iframe src="https://neuronpedia.org/gpt2-small/0-res-jb/14057?embed=true&embedexplanation=true&embedplots=false&embedtest=true" title="Neuronpedia" style={{border: "1px solid #ddd", borderRadius: "10px", width:"480px", height:"300px"}}></iframe>

#### Disabled

`<iframe src="https://neuronpedia.org/gpt2-small/0-res-jb/14057?embed=true&embedexplanation=true&embedplots=false&embedtest=false" title="Neuronpedia" style={{border: "1px solid #ddd", borderRadius: "10px", width:"480px", height:"300px"}}></iframe>`

<iframe src="https://neuronpedia.org/gpt2-small/0-res-jb/14057?embed=true&embedexplanation=true&embedplots=false&embedtest=false" title="Neuronpedia" style={{border: "1px solid #ddd", borderRadius: "10px", width:"480px", height:"300px"}}></iframe>


### Show Plots

Enable or disable showing the two plots by changing query parameter `embedplots` to true or false. This is enabled by default.

`<iframe src="https://neuronpedia.org/gpt2-small/0-res-jb/14057?embed=true&embedexplanation=true&embedplots=false" title="Neuronpedia" style={{border: "1px solid #ddd", borderRadius: "10px", width:"480px", height:"300px"}}></iframe>`

<iframe src="https://neuronpedia.org/gpt2-small/0-res-jb/14057?embed=true&embedexplanation=true&embedplots=false" title="Neuronpedia" style={{border: "1px solid #ddd", borderRadius: "10px", width:"480px", height:"300px"}}></iframe>

### Show Explanation

Enable or disable showing the explanation (usually auto-interp) by changing query parameter `embedexplanation` to true or false. This is enabled by default.

Here's the example above, without explanation:

`<iframe src="https://neuronpedia.org/gpt2-small/0-res-jb/14057?embed=true&embedexplanation=false&embedplots=true" title="Neuronpedia" style={{border: "1px solid #ddd", borderRadius: "10px", width:"480px", height:"300px"}}></iframe>`

<iframe src="https://neuronpedia.org/gpt2-small/0-res-jb/14057?embed=true&embedexplanation=false&embedplots=true" title="Neuronpedia" style={{border: "1px solid #ddd", borderRadius: "10px", width:"480px", height:"300px"}}></iframe>

### Default Activation Text

You can add a default, custom activation text to the embed. Add the query parameter `defaulttesttext` with the URI-encoded string of what you want in the activation field. For example:

`<iframe src="https://neuronpedia.org/gpt2-small/0-res-jb/14057?embed=true&embedexplanation=true&embedplots=true&defaulttesttext=my+custom+Jedi" title="Neuronpedia" style={{border: "1px solid #ddd", borderRadius: "10px", width:"480px", height:"360px"}}></iframe>`
<iframe src="https://neuronpedia.org/gpt2-small/0-res-jb/14057?embed=true&embedexplanation=true&embedplots=true&defaulttesttext=my+custom+Jedi" title="Neuronpedia" style={{border: "1px solid #ddd", borderRadius: "10px", width:"480px", height:"360px"}}></iframe>

## LessWrong Example

LessWrong supports embedding Neuronpedia features directly in the editor. Just copy paste the embed link (not the iframe code) into the editor. Note that the previews will only show up correctly if you copy-paste, not manually type out the url.

Some example links you can directly paste into the editor:
- `https://neuronpedia.org/gpt2-small/0-res-jb/14057?embed=true&embedexplanation=false&embedplots=true&defaulttesttext=the+Jedi`
- `https://neuronpedia.org/gpt2-small/0-res-jb/14057?embed=true&embedexplanation=false`
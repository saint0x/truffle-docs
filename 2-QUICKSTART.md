---
title: 'Quick Start Guide'
description: 'Build your first Truffle app in minutes'
---

# Quick Start Guide

Get up and running with your first Truffle app in under 5 minutes.

## 1. Installation

```bash
pip install https://github.com/deepshard/truffle-sdk-public/releases/download/v0.6.5/truffle_sdk-0.6.4-py3-none-any.whl
```

## 2. Create Your App

```bash
# Initialize a new app
truffle init MyFirstApp
cd MyFirstApp
```

## 3. Implement Your Tool

Open `main.py` and implement your tool:

```python
import truffle
import pandas as pd
import os
from typing import Dict, Any

@truffle.tool(
    description="Process data from a CSV file",
    icon="doc.text.magnifyingglass"  # Uses SF Symbols
)
@truffle.args(
    path="Path to the CSV file to analyze"
)
def analyze_csv(path: str) -> Dict[str, Any]:
    """
    Analyze a CSV file and return its metadata.
    
    Args:
        path: Path to the CSV file
        
    Returns:
        Dict containing file metadata
    """
    if not os.path.exists(path):
        return {"error": f"File not found: {path}"}
        
    df = pd.read_csv(path)
    return {
        "path": path,
        "columns": df.columns.tolist(),
        "shape": df.shape,
        "dtypes": df.dtypes.apply(lambda x: x.name).to_dict()
    }

if __name__ == "__main__":
    app = truffle.TruffleApp(analyze_csv)
    app.launch()
```

## 4. Build and Run

```bash
# Build your app
truffle build

# Your app is now ready to use!
```

## Project Structure

Your app contains:
```
MyFirstApp/
├── main.py           # Your app code
├── manifest.json     # App metadata (auto-generated)
└── requirements.txt  # Dependencies
```

## Key Concepts

1. **Tool Definition**
   - `@truffle.tool`: Main decorator with description and icon
   - `@truffle.args`: Document parameters
   - Type hints for validation
   - Docstrings for documentation

## Available Features

The SDK provides these core features:
- Tool definition with `@truffle.tool` and `@truffle.args`
- Model management with `get_models()`
- Document parsing and embeddings via `query_embed()`
- Perplexity integration with `perplexity_search()`
- Streaming inference with `infer()`
- Real-time tool updates with `tool_update()`
- User interaction with `ask_user()`

## What's Next?

- Read the [SDK Documentation](./SDK-PUBLIC.md) for detailed explanations
- Check out example apps in our [GitHub repository](https://github.com/deepshard/truffle-sdk-public/examples)
- Join our [Discord community](https://discord.gg/truffle) for support

<Note>
Need help? Check our [troubleshooting guide](./TROUBLESHOOTING.md) or join our Discord community.
</Note>

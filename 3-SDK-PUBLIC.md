---
title: 'Truffle SDK'
description: 'Technical documentation for building powerful, composable AI applications'
---

# Truffle SDK Documentation

The Truffle SDK transforms standard Python code into powerful, distributed tools that any Truffle agent can discover and use. This documentation covers the technical details and inner workings of the SDK.

## Core Features

### 1. Tool Definition

Tools are defined using the `@truffle.tool` decorator:

```python
import truffle

@truffle.tool(
    description="Returns metadata given a path to a CSV file",
    icon="tablecells.badge.ellipsis"  # Uses SF Symbols
)
@truffle.args(path="The path to the CSV file to analyze")
def AnalyzeCSV(self, path: str) -> Dict[str, Any]:
    try:
        if not os.path.exists(path):
            return {"error": f"File '{path}' not found"}
        with open(path, 'r') as file:
            df = pd.read_csv(path)
            return {
                "path": path,
                "columns": df.columns.tolist(),
                "shape": df.shape,
                "dtypes": df.dtypes.apply(lambda x: x.name).to_dict()
            }
    except Exception as e:
        return truffle.ReportError(e)
```

### 2. App Metadata

Define your app's metadata:

```python
class MyApp:
    def __init__(self):
        self.metadata = truffle.AppMetadata(
            fullname="My App",        # User-facing name
            description="Description", # User-facing description
            name="myapp",             # Internal name
            goal="App's goal",        # Goal for AI agents
            icon_url="https://..."    # 512x512 PNG icon URL
        )
```

### 3. AI Integration

The SDK provides tools for AI model integration:

```python
@truffle.tool(description="AI-powered analysis")
def AnalyzeText(self, text: str) -> str:
    # Build prompt
    prompt = truffle.PromptBuilder(
        system="Analyze the following text"
    ).Add(text)
    
    # Define response format
    schema = {
        "type": "object",
        "properties": {
            "analysis": {"type": "string"}
        }
    }
    
    # Make inference request
    request = truffle.GenerateRequest(
        id="text_analysis",
        prompt=prompt,
        schema=schema,
        temperature=0.75
    )
    
    # Get response
    response = truffle.InferSync(request, model="yang")
    return json.loads(response)["analysis"]
```

### 4. Vision Processing

Convert images to structured text:

```python
@truffle.tool("Gather data as a CSV or Markdown table")
@truffle.args(as_markdown="Return the data as a markdown table instead of a CSV")
def ProcessTableImage(self, as_markdown: bool) -> str:
    try:
        # Capture image data
        screenshot = get_screenshot()  # Your screenshot logic
        
        # Convert to table format
        format_type = "Markdown" if as_markdown else "CSV"
        return truffle.Vision(
            f"Convert this data to a {format_type} table",
            base64_image=screenshot
        )
    except Exception as e:
        return truffle.ReportError(e)
```

### 5. File Handling

Handle file outputs with `TruffleFile`:

```python
@truffle.tool(description="Generate report")
def BuildReport(self, title: str, data: Dict[str, Any]) -> truffle.TruffleFile:
    content = f"# {title}\n```json\n{data}\n```"
    return truffle.TruffleFile("report.md", content)
```

## Core Components

### 1. Decorators
```python
@truffle.tool(description="...", icon="...")  # Define a tool
@truffle.args(param="description")            # Document parameters
```

### 2. SDK Features
```python
import truffle

# Available features
truffle.AppMetadata      # App metadata definition
truffle.TruffleFile     # File output handling
truffle.PromptBuilder   # AI prompt construction
truffle.GenerateRequest # Inference request creation
truffle.InferSync      # Model inference execution
truffle.Vision         # Image-to-text conversion
truffle.ReportError    # Error reporting
```

### 3. Error Handling
```python
try:
    # Implementation
except Exception as e:
    return truffle.ReportError(e)
```

<Note>
For quick start guide and basic usage, see our [Quick Start Guide](./QUICKSTART.md).
</Note>
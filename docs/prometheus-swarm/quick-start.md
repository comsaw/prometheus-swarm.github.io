---
title: Quick Start Guide
parent: Prometheus Swarm
nav_order: 3
---

This guide will help you get started with Prometheus Swarm quickly.

## Installation

1. First, install the package using pip:

```bash
pip install prometheus-swarm
```

2. Set up your environment variables:

```bash
# For Anthropic Claude
export ANTHROPIC_API_KEY=your_api_key

# For OpenAI
export OPENAI_API_KEY=your_api_key

# For Google Gemini
export GOOGLE_API_KEY=your_api_key
```

## Basic Usage

### 1. Creating an AI Client

```python
from prometheus_swarm.clients import AnthropicClient

# Initialize the client
client = AnthropicClient()

# Make a simple request
response = client.generate("Tell me about artificial intelligence.")
print(response)
```

### 2. Using Workflows

```python
from prometheus_swarm.workflows import BaseWorkflow
from prometheus_swarm.types import WorkflowConfig

class MyWorkflow(BaseWorkflow):
    def __init__(self, config: WorkflowConfig):
        super().__init__(config)

    async def execute(self):
        # Your workflow logic here
        result = await self.client.generate("Your prompt here")
        return result

# Create and run the workflow
config = WorkflowConfig(model="claude-3-opus-20240229")
workflow = MyWorkflow(config)
result = workflow.run()
```

### 3. Using the Database

```python
from prometheus_swarm.database import Database
from sqlmodel import SQLModel, Field

class User(SQLModel, table=True):
    id: int = Field(primary_key=True)
    name: str
    email: str

# Initialize database
db = Database("sqlite:///my_database.db")

# Create tables
db.create_tables()

# Add a user
user = User(name="John Doe", email="john@example.com")
db.add(user)
```

## Next Steps

- Check out the [Configuration Guide](./configuration.md) for detailed setup options
- Explore the [API Reference](./api-reference.md) for complete API documentation
- See [Examples](./examples.md) for more complex usage scenarios

## Common Issues

### API Key Not Found

If you get an error about missing API keys, make sure you've properly set your environment variables.

### Import Errors

Ensure you have all required dependencies installed. You can install optional dependencies using:

```bash
pip install prometheus-swarm[all]
```

### Version Compatibility

Make sure you're using Python 3.8 or later. You can check your Python version using:

```bash
python --version
```

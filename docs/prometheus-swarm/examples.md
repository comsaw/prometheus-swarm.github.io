---
title: Examples
nav_order: 5
---

This page contains practical examples of using Prometheus Swarm in various scenarios.

## Basic Examples

### Simple Text Generation

```python
from prometheus_swarm.clients import AnthropicClient

# Initialize the client
client = AnthropicClient()

# Generate text
response = client.generate("Explain quantum computing in simple terms.")
print(response)
```

### Using Multiple Models

```python
from prometheus_swarm.clients import AnthropicClient, OpenAIClient, GoogleClient

# Initialize clients
anthropic = AnthropicClient()
openai = OpenAIClient()
google = GoogleClient()

# Compare responses
responses = []
prompt = "What is artificial intelligence?"

for client in [anthropic, openai, google]:
    response = client.generate(prompt)
    responses.append(response)
```

## Workflow Examples

### Basic Workflow

```python
from prometheus_swarm.workflows import BaseWorkflow
from prometheus_swarm.types import WorkflowConfig

class SimpleWorkflow(BaseWorkflow):
    def __init__(self, config: WorkflowConfig):
        super().__init__(config)

    async def execute(self):
        # Generate a response
        response = await self.client.generate("Hello, how are you?")
        return response

# Run the workflow
config = WorkflowConfig(model="claude-3-opus-20240229")
workflow = SimpleWorkflow(config)
result = workflow.run()
```

### Chained Workflow

```python
class ChainedWorkflow(BaseWorkflow):
    async def execute(self):
        # First step
        initial_response = await self.client.generate("Generate a story idea.")

        # Second step
        expanded_story = await self.client.generate(
            f"Expand this story idea into a full plot: {initial_response}"
        )

        # Final step
        final_story = await self.client.generate(
            f"Turn this plot into a short story: {expanded_story}"
        )

        return final_story

# Run the workflow
config = WorkflowConfig(
    model="claude-3-opus-20240229",
    temperature=0.8,
    max_tokens=2000
)
workflow = ChainedWorkflow(config)
story = workflow.run()
```

## Database Examples

### Basic Database Operations

```python
from prometheus_swarm.database import Database
from sqlmodel import SQLModel, Field
from typing import Optional

# Define a model
class User(SQLModel, table=True):
    id: Optional[int] = Field(default=None, primary_key=True)
    name: str
    email: str
    age: int

# Initialize database
db = Database("sqlite:///example.db")
db.create_tables()

# Add a user
user = User(name="John Doe", email="john@example.com", age=30)
db.add(user)

# Query users
users = db.query(User).filter(User.age > 25).all()
```

### Database with Workflow

```python
class DatabaseWorkflow(BaseWorkflow):
    def __init__(self, config: WorkflowConfig):
        super().__init__(config)
        self.db = Database(config.database_url)

    async def execute(self):
        # Generate content
        content = await self.client.generate("Generate a user profile.")

        # Parse and store in database
        user_data = self.parse_content(content)
        user = User(**user_data)
        self.db.add(user)

        return user

# Run workflow with database
config = WorkflowConfig(
    model="claude-3-opus-20240229",
    database_url="sqlite:///users.db"
)
workflow = DatabaseWorkflow(config)
new_user = workflow.run()
```

## Advanced Examples

### Retry and Error Handling

```python
from prometheus_swarm.utils import retry
from prometheus_swarm.types import RetryConfig

class RetryWorkflow(BaseWorkflow):
    @retry(max_attempts=3, initial_delay=1, max_delay=10)
    async def execute(self):
        try:
            response = await self.client.generate("Complex query")
            return response
        except Exception as e:
            print(f"Error: {e}")
            raise
```

### Token Management

```python
from prometheus_swarm.tools import TokenCounter

class TokenAwareWorkflow(BaseWorkflow):
    async def execute(self):
        text = "Very long text..."
        token_count = TokenCounter.count_tokens(text, self.config.model)

        if token_count > self.config.max_tokens:
            # Split into chunks
            chunks = TextProcessor.chunk_text(text, self.config.max_tokens)
            responses = []

            for chunk in chunks:
                response = await self.client.generate(chunk)
                responses.append(response)

            return " ".join(responses)

        return await self.client.generate(text)
```

### Custom Model Integration

```python
from prometheus_swarm.types import ModelConfig
from prometheus_swarm.clients import BaseClient

class CustomClient(BaseClient):
    def __init__(self, config: ModelConfig):
        super().__init__(config)

    async def generate(self, prompt: str) -> str:
        # Implement custom API calls
        pass

# Use custom client
config = ModelConfig(
    name="custom-model",
    api_base="https://api.custom.com",
    api_key="your-key"
)
client = CustomClient(config)
response = client.generate("Test prompt")
```

## Web Application Example

### Flask API Integration

```python
from flask import Flask, request, jsonify
from prometheus_swarm.clients import AnthropicClient

app = Flask(__name__)
client = AnthropicClient()

@app.route("/generate", methods=["POST"])
async def generate_text():
    data = request.json
    prompt = data.get("prompt")

    try:
        response = await client.generate(prompt)
        return jsonify({"response": response})
    except Exception as e:
        return jsonify({"error": str(e)}), 500

if __name__ == "__main__":
    app.run(debug=True)
```

### Async Web Application

```python
from aiohttp import web
from prometheus_swarm.clients import AnthropicClient

async def handle_generate(request):
    data = await request.json()
    prompt = data.get("prompt")

    client = AnthropicClient()
    response = await client.generate(prompt)

    return web.json_response({"response": response})

app = web.Application()
app.router.add_post("/generate", handle_generate)

if __name__ == "__main__":
    web.run_app(app)
```

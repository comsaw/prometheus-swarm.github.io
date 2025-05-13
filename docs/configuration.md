---
title: Configuration Guide
---

# Configuration Guide

This guide covers all configuration options available in Prometheus Swarm.

## Environment Variables

Prometheus Swarm uses environment variables for sensitive configuration. You can set these using a `.env` file or system environment variables.

### Required Variables

```bash
# AI Model API Keys
ANTHROPIC_API_KEY=your_anthropic_key
OPENAI_API_KEY=your_openai_key
GOOGLE_API_KEY=your_google_key

# Database Configuration (optional)
DATABASE_URL=your_database_url
```

## WorkflowConfig

The `WorkflowConfig` class is the main configuration object for workflows:

```python
from prometheus_swarm.types import WorkflowConfig

config = WorkflowConfig(
    model="claude-3-opus-20240229",  # AI model to use
    temperature=0.7,                  # Response randomness (0.0-1.0)
    max_tokens=1000,                 # Maximum response length
    database_url="sqlite:///db.sqlite3",  # Database connection string
    retry_attempts=3,                # Number of retry attempts
    timeout=30,                      # Request timeout in seconds
)
```

### Available Models

#### Anthropic Models

- claude-3-opus-20240229
- claude-3-sonnet-20240229
- claude-2.1
- claude-2.0

#### OpenAI Models

- gpt-4-turbo-preview
- gpt-4
- gpt-3.5-turbo

#### Google Models

- gemini-pro
- gemini-pro-vision

## Database Configuration

### SQLite (Default)

```python
from prometheus_swarm.database import Database

db = Database("sqlite:///local.db")
```

### PostgreSQL

```python
db = Database("postgresql://user:password@localhost:5432/dbname")
```

### MongoDB

```python
db = Database("mongodb://localhost:27017/")
```

## Client Configuration

### Anthropic Client

```python
from prometheus_swarm.clients import AnthropicClient

client = AnthropicClient(
    model="claude-3-opus-20240229",
    temperature=0.7,
    max_tokens=1000,
)
```

### OpenAI Client

```python
from prometheus_swarm.clients import OpenAIClient

client = OpenAIClient(
    model="gpt-4-turbo-preview",
    temperature=0.7,
    max_tokens=1000,
)
```

### Google Client

```python
from prometheus_swarm.clients import GoogleClient

client = GoogleClient(
    model="gemini-pro",
    temperature=0.7,
    max_tokens=1000,
)
```

## Logging Configuration

Prometheus Swarm uses Python's built-in logging module. You can configure it like this:

```python
import logging

logging.basicConfig(
    level=logging.INFO,
    format='%(asctime)s - %(name)s - %(levelname)s - %(message)s'
)
```

## Advanced Configuration

### Custom Model Configuration

```python
from prometheus_swarm.types import ModelConfig

model_config = ModelConfig(
    name="custom-model",
    api_base="https://api.custom.com",
    api_key="your-key",
    max_tokens=2000,
)
```

### Retry Configuration

```python
from prometheus_swarm.types import RetryConfig

retry_config = RetryConfig(
    max_attempts=3,
    initial_delay=1,
    max_delay=10,
    exponential_base=2,
)
```

### Workflow Timeout Configuration

```python
from prometheus_swarm.types import TimeoutConfig

timeout_config = TimeoutConfig(
    request_timeout=30,
    workflow_timeout=300,
)
```

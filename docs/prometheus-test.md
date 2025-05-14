---
title: Prometheus Test Framework
---

# Prometheus Test Framework

Prometheus Test is a powerful testing framework designed specifically for testing Prometheus tasks. It provides a structured way to create, configure, and run end-to-end tests for your Prometheus applications.

## Key Features

- **Structured Test Organization**: Define tests using a clear, modular structure
- **Worker Management**: Handle multiple worker instances with different configurations
- **MongoDB Integration**: Built-in support for MongoDB data management
- **Signature Generation**: Utilities for generating wallet signatures
- **Environment Management**: Flexible environment variable handling
- **Step-based Testing**: Define tests as a sequence of clear, manageable steps

## Installation

Install the package using pip:

```bash
pip install prometheus-test
```

The package requires Python 3.8 or later.

## Project Structure

A typical Prometheus test project follows this structure:

```
your-project/
  ├── .env
  ├── src/
  ├── tests/
    ├── .env
    ├── data/
    │    ├── collection1.json
    │    └── collection2.json
    ├── config.yaml
    ├── workers.json
    ├── e2e.py
    ├── steps.py
    └── stages/
      ├── task.py
      ├── submission.py
      └── audit.py
```

## Configuration

### Test Configuration (config.yaml)

The main test configuration file defines test parameters and MongoDB settings:

```yaml
# Test Configuration
task_id: "your_task_id"
base_port: 5000
max_rounds: 3
rounds_collection: "documentations"

# Paths
data_dir: data
workers_config: workers.json

# MongoDB Configuration
mongodb:
  database: your_database_name
  collections:
    tasks:
      data_file: tasks.json
      required_count: 1
    audits:
      required_count: 0
```

### Worker Configuration (workers.json)

Define worker-specific settings including ports, environment variables, and keypairs:

```json
{
	"worker1": {
		"port": 5001,
		"server_entrypoint": "/path/to/entrypoint.py",
		"env_vars": {
			"GITHUB_TOKEN": "WORKER1_GITHUB_TOKEN",
			"GITHUB_USERNAME": "WORKER1_GITHUB_USERNAME"
		},
		"keypairs": {
			"staking": "WORKER1_STAKING_KEYPAIR",
			"main": "WORKER1_PUBLIC_KEYPAIR"
		}
	}
}
```

## Writing Tests

### Test Steps

Tests are organized as a sequence of steps, each representing an API call:

```python
from prometheus_test import TestStep
from stages.step_name import prepare_fn, execute_fn

steps = [
    TestStep(
        name="step_name",
        description="Step description",
        prepare=prepare_fn,
        execute=execute_fn,
        worker="worker_name",
    )
]
```

### Step Functions

Each step consists of two main functions:

1. **Prepare Function**: Sets up data for the API call

```python
def prepare(runner, worker):
    """Setup before step execution"""
    task_id = runner.get("task_id")
    payload = {"data": "example"}

    return {
        "task_id": task_id,
        "signature": create_signature(worker.get_key("main_signing"), payload)
    }
```

2. **Execute Function**: Makes the actual API call

```python
def execute(runner, worker, data):
    """Execute the test step"""
    response = requests.post(f"{worker.get('url')}/endpoint", json=data)

    if not response.ok:
        raise Exception(f"Step failed: {response.text}")

    runner.set("result", response.json())
```

## Running Tests

Create a main test script (`e2e.py`):

```python
from pathlib import Path
from prometheus_test import TestRunner
import dotenv

dotenv.load_dotenv()
from .steps import steps

def main():
    base_dir = Path(__file__).parent
    runner = TestRunner(
        steps=steps,
        config_file=base_dir / "config.yaml"
    )
    runner.run()

if __name__ == "__main__":
    main()
```

## Data Management

### MongoDB Integration

The framework provides built-in support for MongoDB:

```python
# In config.yaml
mongodb:
  database: test_db
  collections:
    tasks:
      data_file: tasks.json
      required_count: 1
```

### Post-Load Processing

You can define a callback for post-processing MongoDB data:

```python
def post_load_callback(db, collections):
    """Process data after loading into MongoDB"""
    for doc in collections["tasks"].find():
        collections["tasks"].update_one(
            {"_id": doc["_id"]},
            {"$set": {"processed": True}}
        )

# In e2e.py
runner = TestRunner(
    steps=steps,
    config_file="config.yaml",
    config_overrides={"post_load_callback": post_load_callback}
)
```

## Utilities

### Signature Generation

Generate wallet signatures for payloads:

```python
from prometheus_test.utils import create_signature

signature = create_signature(
    worker.get_key("main_signing"),
    payload
)
```

### Environment Variables

Access environment variables and worker configuration:

```python
# Get environment variable
api_key = worker.get_env("API_KEY")

# Get worker configuration
worker_url = worker.get("url")

# Get keypair
signing_key = worker.get_key("main_signing")
```

## Best Practices

1. **Modular Organization**: Keep step definitions in separate files under a `stages` directory
2. **Error Handling**: Include proper error handling in execute functions
3. **Skip Conditions**: Add skip conditions for optional steps
4. **Environment Variables**: Use `.env` files for sensitive configuration
5. **Documentation**: Document step purposes and requirements

## Requirements

The framework requires the following main dependencies:

- requests >= 2.25.0
- python-dotenv >= 0.19.0
- pymongo >= 4.0.0
- PyYAML >= 6.0.0
- typing-extensions >= 4.0.0

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

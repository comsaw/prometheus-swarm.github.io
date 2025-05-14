---
title: API Reference
nav_order: 6
---

## Clients

### AnthropicClient

```python
class AnthropicClient:
    """Client for interacting with Anthropic's Claude models."""

    def __init__(self, model: str = "claude-3-opus-20240229", **kwargs):
        """Initialize the Anthropic client.

        Args:
            model (str): The model to use
            **kwargs: Additional configuration options
        """

    async def generate(self, prompt: str) -> str:
        """Generate a response from the model.

        Args:
            prompt (str): The input prompt

        Returns:
            str: The model's response
        """

    async def generate_with_metadata(self, prompt: str) -> Dict[str, Any]:
        """Generate a response with additional metadata.

        Args:
            prompt (str): The input prompt

        Returns:
            Dict[str, Any]: Response and metadata
        """
```

### OpenAIClient

```python
class OpenAIClient:
    """Client for interacting with OpenAI models."""

    def __init__(self, model: str = "gpt-4-turbo-preview", **kwargs):
        """Initialize the OpenAI client.

        Args:
            model (str): The model to use
            **kwargs: Additional configuration options
        """

    async def generate(self, prompt: str) -> str:
        """Generate a response from the model.

        Args:
            prompt (str): The input prompt

        Returns:
            str: The model's response
        """
```

### GoogleClient

```python
class GoogleClient:
    """Client for interacting with Google's Gemini models."""

    def __init__(self, model: str = "gemini-pro", **kwargs):
        """Initialize the Google client.

        Args:
            model (str): The model to use
            **kwargs: Additional configuration options
        """

    async def generate(self, prompt: str) -> str:
        """Generate a response from the model.

        Args:
            prompt (str): The input prompt

        Returns:
            str: The model's response
        """
```

## Workflows

### BaseWorkflow

```python
class BaseWorkflow:
    """Base class for all workflows."""

    def __init__(self, config: WorkflowConfig):
        """Initialize the workflow.

        Args:
            config (WorkflowConfig): Workflow configuration
        """

    async def execute(self) -> Any:
        """Execute the workflow.

        Returns:
            Any: Workflow result
        """

    def run(self) -> Any:
        """Run the workflow synchronously.

        Returns:
            Any: Workflow result
        """
```

## Database

### Database

```python
class Database:
    """Database connection and management."""

    def __init__(self, url: str):
        """Initialize the database connection.

        Args:
            url (str): Database connection URL
        """

    def create_tables(self):
        """Create all defined tables."""

    def add(self, obj: Any):
        """Add an object to the database.

        Args:
            obj (Any): Object to add
        """

    def query(self, model: Type[SQLModel]) -> Query:
        """Create a query for the given model.

        Args:
            model (Type[SQLModel]): Model to query

        Returns:
            Query: Query object
        """
```

## Types

### WorkflowConfig

```python
class WorkflowConfig:
    """Configuration for workflows."""

    def __init__(
        self,
        model: str,
        temperature: float = 0.7,
        max_tokens: int = 1000,
        database_url: Optional[str] = None,
        retry_attempts: int = 3,
        timeout: int = 30,
    ):
        """Initialize workflow configuration.

        Args:
            model (str): Model to use
            temperature (float): Response randomness
            max_tokens (int): Maximum response length
            database_url (Optional[str]): Database connection URL
            retry_attempts (int): Number of retry attempts
            timeout (int): Request timeout in seconds
        """
```

### ModelConfig

```python
class ModelConfig:
    """Configuration for custom models."""

    def __init__(
        self,
        name: str,
        api_base: str,
        api_key: str,
        max_tokens: int = 2000,
    ):
        """Initialize model configuration.

        Args:
            name (str): Model name
            api_base (str): API base URL
            api_key (str): API key
            max_tokens (int): Maximum tokens
        """
```

## Utils

### retry

```python
def retry(
    max_attempts: int = 3,
    initial_delay: float = 1.0,
    max_delay: float = 10.0,
    exponential_base: float = 2.0,
):
    """Retry decorator for failed operations.

    Args:
        max_attempts (int): Maximum retry attempts
        initial_delay (float): Initial delay between retries
        max_delay (float): Maximum delay between retries
        exponential_base (float): Base for exponential backoff
    """
```

### timeout

```python
def timeout(seconds: int = 30):
    """Timeout decorator for operations.

    Args:
        seconds (int): Timeout in seconds
    """
```

## Tools

### TokenCounter

```python
class TokenCounter:
    """Count tokens for different models."""

    @staticmethod
    def count_tokens(text: str, model: str) -> int:
        """Count tokens in text for a specific model.

        Args:
            text (str): Input text
            model (str): Model name

        Returns:
            int: Token count
        """
```

### TextProcessor

```python
class TextProcessor:
    """Process and format text."""

    @staticmethod
    def chunk_text(text: str, chunk_size: int) -> List[str]:
        """Split text into chunks.

        Args:
            text (str): Input text
            chunk_size (int): Maximum chunk size

        Returns:
            List[str]: Text chunks
        """
```

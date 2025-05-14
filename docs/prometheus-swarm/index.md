---
title: Prometheus Swarm
nav_order: 2
---

Prometheus Swarm is a powerful framework for building AI agents, providing a comprehensive suite of tools and utilities for developing, deploying, and managing AI-powered applications.

## Overview

Prometheus Swarm is designed to simplify the process of building AI agents by providing:

- Multiple AI model integrations (Anthropic Claude, OpenAI, Google Gemini)
- Built-in workflow management
- Database integration capabilities
- Utility functions for common AI agent operations
- Type-safe development with comprehensive type hints

## Installation

You can install Prometheus Swarm using pip:

```bash
pip install prometheus-swarm
```

The package requires Python 3.8 or later.

## Key Features

### 1. Multi-Model Support

- Anthropic Claude integration
- OpenAI API support
- Google Gemini AI support
- Extensible client architecture for adding new AI models

### 2. Workflow Management

- Structured workflow definitions
- State management
- Error handling and retry mechanisms

### 3. Database Integration

- Built-in database abstractions
- Support for various database backends
- Data persistence utilities

### 4. Utility Functions

- Type conversion and validation
- Common AI operations
- Helper functions for text processing

### 5. Development Tools

- Debugging utilities
- Testing support
- Development workflow helpers

## Requirements

The framework requires the following main dependencies:

- anthropic >= 0.8.1
- openai >= 0.28.0
- google-genai >= 1.14.0
- pandas >= 2.0.0
- Flask >= 3.0.0
- SQLModel >= 0.0.22
- And various other utilities (see setup.py for complete list)

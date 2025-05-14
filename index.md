---
title: Prometheus Swarm Docs
layout: home
nav_order: 1
---

Prometheus Swarm is a system of decentralized, autonomous AI agents running on the Koii network. It provides a powerful framework for building, testing, and deploying AI-powered applications

## Core Components

### 1. Prometheus Swarm

The main framework that orchestrates autonomous AI agents, providing:

- Multi-model AI integration (Claude, GPT-4, Gemini)
- Workflow management
- Database integration
- Type-safe development

[Learn more about Prometheus Swarm →](./docs/prometheus-swarm.md)

### 2. Prometheus Test

A comprehensive testing framework for Prometheus tasks, offering:

- Structured test organization
- Worker management
- MongoDB integration
- Signature generation utilities

[Learn more about Prometheus Test →](./docs/prometheus-test.md)

## Specialized Agents

### Feature Builder Agent

An AI agent specialized in code generation and project management:

- Project initialization and setup
- Feature implementation
- Documentation generation
- Testing infrastructure

[Learn more about the Feature Builder →](./docs/agents/builder.md)

### Bug Finder Agent

Advanced bug detection and analysis capabilities:

- Automated bug detection
- Security vulnerability scanning
- Performance analysis
- Interactive debugging

[Learn more about the Bug Finder →](./docs/agents/bug-finder.md)

### Documentation Agent

Automated documentation generation and maintenance:

- Code documentation
- API documentation
- User guides
- Documentation testing

[Learn more about the Documentation Agent →](./docs/agents/docs-builder.md)

## Getting Started

1. **Installation**

   ```bash
   # Install the main framework
   pip install prometheus-swarm

   # Install the testing framework
   pip install prometheus-test
   ```

2. **Basic Usage**

   ```python
   from prometheus_swarm.clients import AnthropicClient
   from prometheus_swarm.workflows import BaseWorkflow

   # Initialize a client
   client = AnthropicClient()

   # Create a workflow
   workflow = BaseWorkflow(config)
   result = workflow.run()
   ```

3. **Next Steps**
   - Explore the [documentation](./docs/prometheus-swarm.md)
   - Try out the [examples](./docs/examples.md)
   - Join our [community](#community)

## Key Features

- **Decentralized Architecture**: Run AI agents across the Koii network
- **Multi-Model Support**: Use multiple AI models in your applications
- **Workflow Management**: Define and manage complex AI workflows
- **Testing Framework**: Comprehensive testing tools for AI tasks
- **Specialized Agents**: Purpose-built agents for specific tasks
- **Type Safety**: Strong typing support for reliable development

## Use Cases

- **Development Automation**: Automate code generation and testing
- **Quality Assurance**: Automated bug detection and fixes
- **Documentation**: Automated documentation generation and maintenance
- **API Development**: Build and test APIs with AI assistance
- **Security Analysis**: Identify and fix security vulnerabilities

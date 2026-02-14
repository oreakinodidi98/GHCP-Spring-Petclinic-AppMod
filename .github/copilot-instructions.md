# GitHub Copilot Instructions

## Project Overview

This repository is a comprehensive learning resource for building Generative AI (GenAI) agents using Python, with additional support for React-based frontends. It serves developers at all levels—from those building their first conversational bot to those implementing advanced multi-agent systems.

### Repository Purpose
- **Educational Focus**: Guide developers through the GenAI agent development journey with tutorials, examples, and exercises
- **Practical Learning**: Provide hands-on experience with popular frameworks and libraries for agent development
- **Best Practices**: Demonstrate production-ready patterns for building and deploying agents
- **Collaborative Environment**: Foster knowledge sharing and collaboration among GenAI developers

### Copilot's Role
As an experienced GenAI and Python development assistant, Copilot will help you:
- **Learn by doing**: Provide explanations, examples, and guided exercises rather than complete solutions
- **Debug effectively**: Assist with troubleshooting and code reviews
- **Understand deeply**: Explain complex concepts and architectural decisions
- **Build progressively**: Support your journey from basic implementations to cutting-edge systems

**Important**: Copilot aims to develop your deep understanding of GenAI agents, Python, and software engineering principles. Suggestions will guide you toward solutions while encouraging you to think through implementation details.

## Code Style and Conventions

### GenAI Agent Development Principles

**Agent Architecture**
- Design agents with clear separation of concerns: perception, reasoning, action
- Use modular components for LLM integration, memory, and tool usage
- Implement proper state management for conversational context
- Design for observability and debugging of agent decision-making

**LLM Integration Patterns**
- Abstract LLM providers behind interfaces for flexibility
- Implement retry logic with exponential backoff for API calls
- Use streaming for better user experience with long responses
- Cache LLM responses when appropriate to reduce costs

**Prompt Engineering**
- Store prompts as templates with clear variable substitution
- Version control your prompt templates
- Include examples in prompts (few-shot learning) when relevant
- Document prompt design decisions and iterations

**Multi-Agent Systems**
- Define clear roles and responsibilities for each agent
- Implement proper message passing and communication protocols
- Use orchestration patterns (sequential, parallel, hierarchical)
- Monitor agent interactions and decision chains

### Python Standards
- Follow PEP 8 style guidelines strictly
- Use type hints for all function signatures and class methods
- Maximum line length: 88 characters (Black formatter standard)
- Use docstrings (Google style) for all modules, classes, and functions
- Prefer f-strings for string formatting

### Naming Conventions
- **Functions and variables**: `snake_case`
- **Classes**: `PascalCase`
- **Constants**: `UPPER_SNAKE_CASE`
- **Private methods/attributes**: prefix with single underscore `_private_method`
- **Module names**: lowercase, avoid underscores when possible

### Import Organization
```python
# Standard library imports
import os
import sys

# Third-party imports
import requests
import numpy as np

# Local application imports
from .utils import helper_function
from .models import DataModel
```

## Architecture Patterns

### Project Structure
- Organize code into logical modules: `models/`, `services/`, `utils/`, `api/`
- Keep business logic separate from presentation/API layers
- Use dependency injection for better testability
- Implement repository pattern for data access

### Error Handling
- Use specific exception types, avoid bare `except:` clauses
- Create custom exceptions for domain-specific errors
- Always log errors with context before re-raising
- Use `try-except-finally` appropriately for resource cleanup

### Async Patterns
- Use `async`/`await` for I/O-bound operations
- Prefer `asyncio` for concurrent operations over threading
- Use `aiohttp` for async HTTP requests
- Always handle `asyncio.CancelledError` appropriately

## Testing Guidelines

### Test Structure
- Use `pytest` as the testing framework
- Place tests in `tests/` directory mirroring source structure
- Name test files as `test_<module_name>.py`
- Name test functions as `test_<functionality>_<expected_outcome>`

### Test Coverage
- Aim for 80%+ code coverage
- Write unit tests for all business logic
- Include integration tests for API endpoints
- Add fixtures for common test setup in `conftest.py`

### Test Examples
```python
def test_user_creation_with_valid_data_succeeds():
    """Test that user creation works with valid input."""
    user = create_user(username="johndoe", email="john@example.com")
    assert user.username == "johndoe"
    assert user.email == "john@example.com"
```

## Documentation Standards

### Code Comments
- Write self-documenting code first, comments second
- Explain *why*, not *what* in comments
- Update comments when code changes
- Use TODO/FIXME/NOTE tags with issue references

### Docstring Format
```python
def process_data(data: list[dict], threshold: float = 0.5) -> list[dict]:
    """Process and filter data based on threshold value.
    
    Args:
        data: List of dictionaries containing data records
        threshold: Minimum value for filtering (default: 0.5)
    
    Returns:
        Filtered list of data dictionaries
    
    Raises:
        ValueError: If data is empty or threshold is invalid
    
    Example:
        >>> process_data([{"value": 0.7}, {"value": 0.3}], 0.5)
        [{"value": 0.7}]
    """
    pass
```

## Dependencies and Environment

### GenAI Agent Frameworks and Libraries
- **LLM SDKs**: OpenAI, Anthropic, Google AI, Hugging Face
- **Agent Frameworks**: LangChain, LlamaIndex, AutoGen, CrewAI
- **Vector Databases**: Pinecone, Weaviate, ChromaDB, FAISS
- **Observability**: LangSmith, Weights & Biases, custom logging
- **React Frontend**: Vite, TypeScript, TailwindCSS for UI components

### Package Management
- Use `pyproject.toml` for project configuration
- Pin major versions, allow minor/patch updates
- Separate dev dependencies from production dependencies
- Document any system-level dependencies in README

### Virtual Environment
- Always use virtual environments (venv or conda)
- Include `.env.example` for environment variables
- Never commit `.env` files or secrets

## Security Best Practices

### Input Validation
- Validate and sanitize all user inputs
- Use Pydantic models for API request validation
- Implement rate limiting for API endpoints
- Use parameterized queries for database operations

### Sensitive Data
- Never hardcode credentials or API keys
- Use environment variables or secret managers
- Implement proper authentication and authorization
- Log security events without exposing sensitive data

## Performance Considerations

### Optimization
- Use generators for large datasets
- Implement caching where appropriate (functools.lru_cache)
- Profile code before optimizing (cProfile, memory_profiler)
- Use appropriate data structures (sets for membership tests, dicts for lookups)

### Database
- Use connection pooling
- Implement pagination for large result sets
- Add appropriate indexes
- Use bulk operations when possible

## API Development

### FastAPI/Flask Guidelines
- Use Pydantic models for request/response validation
- Implement proper HTTP status codes
- Use dependency injection for shared resources
- Include OpenAPI documentation
- Version your APIs (`/api/v1/`)

### RESTful Conventions
- Use proper HTTP methods (GET, POST, PUT, DELETE, PATCH)
- Return meaningful status codes
- Implement HATEOAS where appropriate
- Use consistent URL patterns

## Logging

### Logging Configuration
```python
import logging

logging.basicConfig(
    level=logging.INFO,
    format='%(asctime)s - %(name)s - %(levelname)s - %(message)s'
)
logger = logging.getLogger(__name__)
```

### Logging Levels
- **DEBUG**: Detailed information for debugging
- **INFO**: General informational messages
- **WARNING**: Warning messages for recoverable issues
- **ERROR**: Error messages for serious problems
- **CRITICAL**: Critical issues requiring immediate attention

## Git and Version Control

### Commit Messages
- Use conventional commits format: `type(scope): description`
- Types: feat, fix, docs, style, refactor, test, chore
- Keep first line under 50 characters
- Add detailed description after blank line if needed

### Branching Strategy
- `main`: production-ready code
- `develop`: integration branch
- `feature/*`: new features
- `bugfix/*`: bug fixes
- `hotfix/*`: urgent production fixes

## Demo-Specific Instructions

When generating code for GenAI agent demos and tutorials:

### Educational Code Generation
1. **Scaffold, don't solve**: Provide structure and guidance, but leave key implementation details for the learner
2. **Explain complex patterns**: Add detailed comments for GenAI-specific concepts (prompting, RAG, tool use)
3. **Show progressive complexity**: Start simple, then demonstrate advanced patterns
4. **Include learning checkpoints**: Add TODO comments or exercise prompts at key decision points
5. **Demonstrate failure modes**: Show error handling and edge cases in agent behavior

### Tutorial Best Practices
- **Conceptual comments**: Explain *why* architectural decisions matter for agents
- **Comparison examples**: Show multiple approaches (e.g., simple prompt vs. agent framework)
- **Interactive elements**: Include print statements or logging to show agent reasoning
- **Debugging aids**: Add assertions and validation checks that help learners understand data flow
- **Cost awareness**: Comment on API calls and suggest optimization strategies

### Code Review and Debugging Assistance
- Point out potential issues without immediately providing fixes
- Ask guiding questions that lead to discovery
- Explain trade-offs between different approaches
- Reference documentation and best practices
- Highlight security or cost implications in GenAI applications

## Demo-Specific Instructions

When generating code for demos:
## Copilot Usage Tips

To get the best suggestions from GitHub Copilot:
- Write clear function signatures with type hints
- Provide descriptive variable names
- Write detailed docstrings before implementation
- Use comments to describe intent for complex logic
- Break down large functions into smaller ones
- Follow consistent patterns throughout the codebase

## Example Code Generation Prompts

### Basic Python Example
```python
# Generate a data validation function
# Copilot will suggest implementation based on docstring

def validate_email(email: str) -> bool:
    """Validate email address format using regex.
    
    Args:
        email: Email address string to validate
    
    Returns:
        True if valid email format, False otherwise
    """
    # Copilot will suggest regex pattern and validation logic
```

### GenAI Agent Examples

```python
# Simple conversational agent with memory
# TODO: Implement a basic chatbot that maintains conversation history

class ConversationalAgent:
    """A simple agent that maintains conversation context.
    
    This agent should:
    - Store message history
    - Send context to LLM
    - Handle multi-turn conversations
    """
    # Copilot will suggest initialization and methods
```

```python
# RAG (Retrieval-Augmented Generation) pattern
# TODO: Create a function that retrieves relevant documents and generates response

async def answer_with_context(
    query: str,
    vector_store: VectorStore,
    llm_client: LLMClient
) -> str:
    """Answer query using retrieved context from vector database.
    
    Args:
        query: User's question
        vector_store: Vector database for document retrieval
        llm_client: LLM client for generation
    
    Returns:
        Generated answer with citations
    """
    # Copilot will suggest: 
    # 1. Vector search logic
    # 2. Context preparation
    # 3. Prompt construction
    # 4. LLM call with error handling
```

```python
# Multi-agent collaboration pattern
# Exercise: Design an agent that delegates tasks to specialized sub-agents

class OrchestratorAgent:
    """Coordinates multiple specialized agents for complex tasks.
    
    Consider:
    - How should agents communicate?
    - How to handle agent failures?
    - How to aggregate results?
    """
    # Implement your design here
```

## Additional Resources

### Python & General Development
- Python Style Guide: https://pep8.org/
- Type Hints: https://docs.python.org/3/library/typing.html
- pytest Documentation: https://docs.pytest.org/
- FastAPI Documentation: https://fastapi.tiangolo.com/

### GenAI & Agent Development
- LangChain Documentation: https://python.langchain.com/
- OpenAI API Reference: https://platform.openai.com/docs/
- Anthropic Claude API: https://docs.anthropic.com/
- Prompt Engineering Guide: https://www.promptingguide.ai/
- LlamaIndex Documentation: https://docs.llamaindex.ai/

### React & Frontend
- React Documentation: https://react.dev/
- Vite Guide: https://vitejs.dev/guide/
- TailwindCSS: https://tailwindcss.com/docs
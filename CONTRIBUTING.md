# Contributing to RAG Systems Production

Thank you for your interest in contributing to RAG Systems Production! This document provides guidelines and instructions for contributing.

## Table of Contents

- [Code of Conduct](#code-of-conduct)
- [Getting Started](#getting-started)
- [Development Setup](#development-setup)
- [Contributing Guidelines](#contributing-guidelines)
- [Pull Request Process](#pull-request-process)
- [Testing Requirements](#testing-requirements)

## Code of Conduct

Please read and follow our [Code of Conduct](CODE_OF_CONDUCT.md).

## Getting Started

### Prerequisites

- Python 3.8+
- Node.js 16+
- Docker
- Git
- API keys for:
  - OpenAI or Cohere (embeddings)
  - Vector store (Pinecone, Weaviate, etc.)
  - LLM provider (OpenAI, Anthropic, etc.)

### Setting Up Your Development Environment

1. **Fork and clone the repository**

   ```bash
   git clone https://github.com/groovy-web/rag-systems-production.git
   cd rag-systems-production
   ```

2. **Set up Python environment**

   ```bash
   python -m venv venv
   source venv/bin/activate  # On Windows: venv\Scripts\activate
   pip install -r requirements.txt
   pip install -r requirements-dev.txt
   ```

3. **Set up Node environment**

   ```bash
   npm install
   ```

4. **Configure environment variables**

   ```bash
   cp .env.example .env
   # Edit .env with your API keys
   ```

5. **Run tests**

   ```bash
   npm test
   pytest
   ```

## Development Setup

### Architecture Overview

The system is organized into:

- **Ingestion**: Document processing and chunking
- **Embedding**: Vector embedding generation
- **Retrieval**: Search and retrieval strategies
- **Generation**: LLM integration and response generation
- **API**: REST API endpoints
- **Monitoring**: Metrics and observability

### Development Workflow

1. **Create a feature branch**

   ```bash
   git checkout -b feature/your-feature
   ```

2. **Make your changes**

   - Write code
   - Add tests
   - Update documentation

3. **Test locally**

   ```bash
   npm run lint
   npm test
   pytest
   npm run build
   ```

4. **Commit and push**

   ```bash
   git add .
   git commit -m "feat: add description"
   git push origin feature/your-feature
   ```

## Contributing Guidelines

### What to Contribute

We welcome contributions in:

- **New Retrieval Strategies**: Novel retrieval approaches
- **Vector Store Integrations**: Support for new vector databases
- **Embedding Models**: Additional embedding providers
- **Performance Improvements**: Optimization and scaling
- **Documentation**: Guides, tutorials, API docs
- **Tests**: Unit tests, integration tests, benchmarks
- **Bug Fixes**: Resolving issues

### Contribution Areas

#### 1. Retrieval Strategies

Add new retrieval methods to `src/retrieval/`:

```python
class CustomRetrievalStrategy(BaseRetrievalStrategy):
    def retrieve(self, query, top_k=10):
        # Implementation here
        pass
```

#### 2. Vector Stores

Add new vector store support in `src/vector_stores/`:

```python
class NewVectorStore(BaseVectorStore):
    def __init__(self, config):
        # Implementation here
        pass
```

#### 3. Embedding Models

Add new embedding providers in `src/embeddings/`:

```python
class NewEmbeddingModel(BaseEmbeddingModel):
    def embed(self, text):
        # Implementation here
        pass
```

### Code Style

#### Python Style Guide

Follow PEP 8 and use:

```python
# Type hints
def process_document(doc: Document) -> ProcessedDocument:
    pass

# Docstrings
def retrieve(query: str, top_k: int = 10) -> List[Document]:
    """
    Retrieve documents based on query.

    Args:
        query: Search query string
        top_k: Number of results to return

    Returns:
        List of retrieved documents
    """
    pass

# Error handling
try:
    result = vector_store.query(query)
except VectorStoreError as e:
    logger.error(f"Query failed: {e}")
    raise
```

#### JavaScript/TypeScript Style

Use ESLint and Prettier:

```typescript
// Type definitions
interface RetrievalConfig {
  topK: number;
  threshold: number;
}

// Error handling
async function retrieve(
  query: string,
  config: RetrievalConfig
): Promise<Document[]> {
  try {
    return await vectorStore.query(query, config);
  } catch (error) {
    logger.error(`Query failed: ${error}`);
    throw error;
  }
}
```

### Documentation Standards

All code must include:

1. **Docstrings**: Describe purpose, parameters, returns
2. **Comments**: Explain complex logic
3. **Examples**: Show usage in README
4. **Changelog**: Update CHANGELOG.md

### Testing Requirements

#### Unit Tests

```python
def test_retrieval_strategy():
    strategy = CustomRetrievalStrategy()
    results = strategy.retrieve("test query")
    assert len(results) > 0
    assert all(isinstance(r, Document) for r in results)
```

#### Integration Tests

```python
def test_end_to_end_retrieval():
    engine = RAGEngine(config)
    engine.ingest(["test.pdf"])
    response = engine.query("test question")
    assert response.answer is not None
    assert len(response.sources) > 0
```

#### Performance Tests

```python
def test_retrieval_performance():
    strategy = VectorStoreStrategy()
    start = time.time()
    results = strategy.retrieve("query", top_k=100)
    duration = time.time() - start
    assert duration < 1.0  # Should complete in < 1 second
```

### Commit Message Format

Follow conventional commits:

```
<type>(<scope>): <description>

[optional body]

[optional footer]
```

**Types**: `feat`, `fix`, `docs`, `style`, `refactor`, `test`, `perf`, `chore`

**Examples**:

```
feat(retrieval): add hybrid search with reranking

fix(vector-store): resolve Pinecone connection timeout

docs: update deployment guide with Kubernetes

perf(embedding): implement batch processing

test: add integration tests for Weaviate
```

## Pull Request Process

### 1. Before Creating PR

- [ ] Code follows style guidelines
- [ ] Tests added and passing
- [ ] Documentation updated
- [ ] Changelog updated
- [ ] No merge conflicts

### 2. Creating PR

1. **Descriptive title**
   - Use conventional commit format
   - Example: "feat(retrieval): add hybrid search"

2. **Detailed description**
   - What changes were made
   - Why changes were needed
   - How it works
   - Breaking changes (if any)

3. **Linked issues**
   - Reference related issues
   - Use keywords: "Fixes #123", "Closes #456"

4. **Screenshots/Demos**
   - For UI changes
   - For new features

### 3. PR Template

```markdown
## Description
Brief description of changes

## Type of Change
- [ ] Bug fix
- [ ] New feature
- [ ] Breaking change
- [ ] Documentation update
- [ ] Performance improvement

## Testing
- [ ] Unit tests added
- [ ] Integration tests added
- [ ] All tests pass
- [ ] Manual testing completed

## Documentation
- [ ] API docs updated
- [ ] README updated
- [ ] Examples added
- [ ] Changelog updated

## Checklist
- [ ] Code follows style guide
- [ ] Self-review completed
- [ ] Comments added
- [ ] No new warnings
- [ ] Performance tested
```

### Review Process

#### What We Review

1. **Correctness**
   - Logic is sound
   - Edge cases handled
   - Error handling proper

2. **Performance**
   - Efficient algorithms
   - No memory leaks
   - Scalability considered

3. **Security**
   - No API keys exposed
   - Input validation
   - Proper authentication

4. **Documentation**
   - Clear and accurate
   - Examples provided
   - API docs complete

#### Timeline

- Initial review: 2-3 days
- Additional rounds: 3-5 days each
- Complex features: 1-2 weeks

## Testing Guidelines

### Local Testing

```bash
# Run all tests
npm test
pytest

# Run specific test suite
npm test -- --grep "retrieval"
pytest tests/test_retrieval.py

# Run with coverage
npm run test:coverage
pytest --cov=src tests/

# Run integration tests
npm run test:integration
pytest tests/integration/
```

### Performance Benchmarks

```bash
# Run benchmarks
npm run benchmark

# Compare with baseline
npm run benchmark -- --compare
```

### Before Submitting

1. **Lint code**
   ```bash
   npm run lint
   flake8 src/
   black --check src/
   ```

2. **Format code**
   ```bash
   npm run format
   black src/
   ```

3. **Run tests**
   ```bash
   npm test
   pytest
   ```

4. **Build project**
   ```bash
   npm run build
   python setup.py build
   ```

## Feature Proposal Process

For major features:

1. **Open a discussion** first
2. **Get feedback** from maintainers
3. **Create proposal** document
4. **Get approval** before implementing

## Release Process

Maintainers handle releases:

1. Update version number
2. Update CHANGELOG.md
3. Create git tag
4. Publish to npm/PyPI
5. Create GitHub release

## Getting Help

### Resources

- [Documentation](docs/)
- [API Reference](docs/api-reference.md)
- [Examples](examples/)

### Community

- GitHub Issues: Bug reports, questions
- GitHub Discussions: Ideas, proposals
- Discord: Real-time chat (link in docs)

### Contact Maintainers

- Create a GitHub issue
- Mention @maintainer in discussions
- Email: maintainers@example.com

## Recognition

Contributors will be:
- Listed in CONTRIBUTORS.md
- Mentioned in release notes
- Invited to contributor Discord channel

## License

By contributing, you agree that your contributions will be licensed under the Apache 2.0 License.

## Questions?

- Check existing issues and discussions
- Read documentation thoroughly
- Ask in GitHub Discussions

Thank you for contributing to RAG Systems Production!

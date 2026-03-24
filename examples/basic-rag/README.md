# Basic RAG System Example

A simple Retrieval-Augmented Generation (RAG) system implementation for learning and testing.

## Overview

This example demonstrates a minimal RAG system that:
1. Ingests text documents
2. Generates vector embeddings
3. Performs semantic search
4. Generates AI responses with context

## Prerequisites

- Python 3.8+
- OpenAI API key
- pip

## Installation

```bash
# Install dependencies
pip install openai python-dotenv numpy

# Set up environment
cp .env.example .env
# Edit .env and add your OpenAI API key
```

## Quick Start

### 1. Prepare Documents

Create text files in the `documents/` directory:

```bash
echo "Python is a high-level programming language." > documents/doc1.txt
echo "JavaScript is used for web development." > documents/doc2.txt
echo "Machine learning is a subset of AI." > documents/doc3.txt
```

### 2. Run the RAG System

```bash
python rag_system.py
```

### 3. Ask Questions

```
Enter your question (or 'quit' to exit): What is Python?
Searching documents...
Found relevant context: Python is a high-level programming language.

AI Response: Python is a high-level programming language.

Enter your question (or 'quit' to exit): quit
Goodbye!
```

## Key Concepts

### Document Chunking

Documents are split into smaller chunks for better retrieval.

### Vector Embeddings

Text is converted to numerical vectors for semantic search.

### Semantic Search

Find similar documents using cosine similarity.

### Context-Aware Generation

Use retrieved context to generate AI responses.

## Customization

### Use Different Embedding Model

Edit `config.py`:
```python
EMBEDDING_MODEL = "text-embedding-3-small"  # Cheaper, faster
```

### Adjust Chunk Size
```python
CHUNK_SIZE = 1000  # Larger chunks
CHUNK_OVERLAP = 100  # More overlap
```

## Next Steps

1. Add more documents
2. Improve chunking strategy
3. Add reranking
4. Build web interface
5. Deploy as API

## Resources

- [Main Documentation](../../docs/architecture.md)
- [OpenAI API](https://platform.openai.com/docs/)

## License

Apache 2.0 License

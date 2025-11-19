# GraphRAG Knowledge Graph (Documentation Only)

This repo documents a personal project where I built a small **GraphRAG-style system** from scratch.

The actual implementation code (Python scripts, SQL, Docker setup) is **kept private**.  
This repo is meant to explain **what the system does, how it’s structured, and what I learned**, without exposing the source code.

---

## What This Project Does

At a high level:

- Chunked a book using ChatGPT
- Ran each chunk through a MiniLM embedding model (384-dim vectors)
- Stored embeddings + metadata in PostgreSQL with **pgvector**
- Build a simple **knowledge graph** (nodes = chunks, edges = relationships)
- Support **vector similarity search** for retrieval

This was built to understand how GraphRAG systems actually work behind the scenes.

---

## Tech Stack

 The stack behind the project is:

- **Python**
- **SentenceTransformers** (MiniLM embedding model)
- **PostgreSQL + pgvector**
- **psycopg2-binary**
- **Docker Compose**

Everything else (chunking logic, ingestion scripts, edge builder, query runner) is custom code kept private.

---

## System Overview

### 1. Chunking
The document is split into smaller, meaningful chunks with metadata like:

- page number  
- type (concept, definition, example, etc.)

> **Transparency:** For this prototype, I had ChatGPT chunk a public copy of *Atomic Habits* so I could focus on embeddings, vector search, and the graph structure. Future versions will use a custom Python chunker.

---

### 2. Embedding
Chunks are encoded using a 384-dim MiniLM model:

```
from sentence_transformers import SentenceTransformer
model = SentenceTransformer("all-MiniLM-L6-v2")
embedding = model.encode(chunk_text)
These embeddings power similarity search.
```
## 3. Storage (pgvector + Postgres)
   
Two main tables:

  - vertices (chunks + embeddings)

  - edges (relationships between chunks)

The embedding column uses the pgvector type.

## 4. Vector Search

Given a user query:

It’s embedded into a vector. The system runs a pgvector similarity search, and the top-k results (closest chunks) are returned.

Conceptually:

```
SELECT id, text
FROM vertices
ORDER BY embedding <-> $1
LIMIT 10;
```
# 5. Knowledge Graph
Edges connect related chunks using:

  - similarity thresholds

  - metadata-driven rules

  - concept ↔ definition links

This produces a lightweight knowledge graph over the text.

## Dataset Transparency
The prototype uses public copy of Atomic Habits. The chunks generated with ChatGPT (to speed up early development).

This let me focus on:

  - pgvector setup
  
  - embedding generation
  
  - graph building
  
  - retrieval logic

Future work will replace this with a custom chunker + new datasets.


# Why I Built This

I wanted to understand:

 - how to use SQL/Postgres SQL
 -  how embeddings are stored and queried
 - how vector search works
 - how a graph layer can sit on top of embeddings
 - what “GraphRAG” really means at a systems level


# What’s in This Repo

This repo is documentation-only:

```
README.md
docs/
  ├── architecture.md
  ├── dataset-notes.md
  └── future-roadmap.md
The implementation code is private.
```

Documentation

See the docs/ folder for:

architecture.md — system design & flow

dataset-notes.md — chunking and data transparency

future-roadmap.md — where I want to take this project next

🔗 Contact
If you’d like to discuss the project or see a walkthrough of the private implementation, feel free to reach out.

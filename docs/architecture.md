# Architecture Overview

This file explains the main components of the GraphRAG knowledge graph system.

---

## High-Level Components

### 1. Embedding Generation
- MiniLM model via SentenceTransformers  
- 384-dim embeddings  
- Python-based

### 2. Storage Layer (PostgreSQL + pgvector)
- Stores:
  - text chunks  
  - embeddings  
  - metadata  
- Provides vector search  
- Stores graph edges

### 3. Graph Builder
- Calculates similarity  
- Creates edges using:
  - similarity threshold  
  - metadata rules  
  - simple heuristics  

### 4. Query Layer
- Embeds user query  
- Runs pgvector KNN search  
- Optionally expands via graph neighbors

---

## Data Flow (Text Diagram)

Chunked Text File -> Embeddings (MiniLM) -> Create the relationship tables

Similarity Engine → Edges (graph)

Query → Embedding → Similarity Search → Results

---

## Database Schema (Conceptual)

### `vertices`

| column        | type        | description           |
|---------------|-------------|-----------------------|
| id            | int         | unique ID             |
| text          | text        | chunk text            |
| embedding     | vector (384)| chunk embedding       |
| source_page   | int         | page or section       |
| chunk_type    | text        |concept/definition/etc |

---

### `Edges`

| column           | type   | description         |
|------------------|--------|---------------------|
| id               | int    | edge id             |
| source_id        | int    | from node           |
| target_id        | int    | to node             |
| relationship_type| text   | semantic relation   |
| similarity_score | float  | cosine similarity   |

---


(Side Note I wanted to do this locally because I could really see what these relationships look like and it's free lol)

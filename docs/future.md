# Future Roadmap

These are the next steps I want to explore as the project grows.

---

## Chunking & Data

- Build a Python chunker:
  - token-aware  
  - overlapping windows  
  - richer metadata  
- Apply it to:
  - technical texts  
  - USMLE-style textbooks (study only)  
  - clinical-style question generation for learning

---

## LLM Integration

- Connect the system to **Ollama**
  - Use local LLMs on top of vector search + graph  
- Experiment with:
  - different local models  
  - prompting strategies  
  - graph-augmented generation  

---

## UI & API

- Build a **React UI**:
  - chat interface  
  - graph visualization  
- Add a **REST API** for:
  - nearest neighbor search  
  - node neighbors  
  - graph traversal  

---

## Infra & Performance

- Add **Redis** for caching  
- Deploy to **Google Cloud Run**  
- Containerize all components cleanly  

---

## Embedding Models

- Try larger embedding models  
- Compare performance + quality  
- Explore domain-specific models later  

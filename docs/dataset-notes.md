# Dataset & Chunking Notes

This project is not tied to a specific dataset.  
For the prototype, I used a **public copy of **Atomic Habits** to test chunking, embeddings, and the graph.

---

## Why Atomic Habits?

- Never read it before but I wanted to see how ingetsing chunks works.
---

## Chunking Method (Prototype)

For transparency:

- I used **ChatGPT** to generate the initial chunks  
- This allowed fast progress on:
  - embedding logic  
  - pgvector setup  
  - database schema  
  - graph construction  

This prototype method will be replaced with a custom chunker.

---

## Future Chunking Plans

A custom Python chunker will support:

- token-based windows  
- overlapping chunks  
- metadata extraction  
- chapter / section tagging  

Use cases I want to explore:

- Technical textbooks  
- USMLE-style study content (for learning only)  
- Clinical-style question generation  

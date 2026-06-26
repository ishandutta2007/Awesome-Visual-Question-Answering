# Outside-Knowledge VQA (OK-VQA)

**Knowledge-Based or Outside-Knowledge Visual Question Answering (OK-VQA)** focuses on questions that cannot be resolved solely by parsing visual pixels; they require cross-referencing visual details with external facts, commonsense, or encyclopedic knowledge databases.

---

## 🏛️ System Architecture & Retrieval Pipeline

OK-VQA models usually deploy a **Retrieval-Augmented Generation (RAG)** pipeline. First, the image and question are processed to extract entities or search terms. These are queried against an external Knowledge Base (KB) such as Wikipedia or ConceptNet. The retrieved passages are fused with visual/text embeddings to generate the final response.

```mermaid
flowchart TD
    %% Define Nodes
    Img[Input Image] & Que[Question] --> Parser[Entity & Query Extractor]
    Parser --> Search[Search Query]
    Search --> KB[(External Knowledge Base<br/>Wikipedia / ConceptNet / Wikidata)]
    
    KB --> Docs[Retrieved Facts & Passages]
    Docs --> Fusion[Multimodal Reasoning Core]
    Img & Que --> Fusion
    
    Fusion --> Generator[Answer Generator]
    Generator --> Ans[Final Knowledge-Grounded Answer]
    
    %% Style Nodes
    classDef default fill:#1e1e2e,stroke:#cdd6f4,stroke-width:1px,color:#cdd6f4;
    classDef accent fill:#eba0ac,stroke:#cdd6f4,stroke-width:2px,color:#11111b;
    class Ans accent;
```

---

## 🛠️ Key Techniques & Paradigms

1. **Explicit Retrieval (RAG):** Querying external vector stores or search engines using text queries generated from image descriptions.
2. **Implicit Retrieval (Parametric Knowledge):** Relying on massive foundation Large Language Models (LLMs) which have encyclopedic facts memorized directly within their parameters.
3. **Multimodal Concept Mapping:** Aligning visual regions with semantic entities in knowledge graphs (e.g., linking a photo of a specific bird species to its habitat and diet information).

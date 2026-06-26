# Document VQA (DocVQA)

**Document Visual Question Answering (DocVQA)** is a specialized subfield of VQA focused on parsing information from text-dense images, corporate documents, PDFs, invoices, forms, charts, and table grids.

---

## 🏛️ System Architecture & Multimodal Processing

DocVQA architectures must merge three modalities: **Visual pixels**, **OCR text tokens**, and **2D spatial layout coordinates** (bounding boxes). The fusion is typically processed using layout-aware transformers (like LayoutLM).

```mermaid
flowchart TD
    %% Define Nodes
    Doc[Document Image] --> OCR[OCR Engine]
    Doc --> Vision[Vision Encoder]
    
    OCR --> Text[Extracted Text Tokens]
    OCR --> BBox[2D Layout Coordinates]
    Vision --> Visual[Visual Representation]
    
    Text --> Fusion[Layout-Aware Multimodal Transformer<br/>e.g., LayoutLM / LMM]
    BBox --> Fusion
    Visual --> Fusion
    
    Que[Layout Query] --> Fusion
    Fusion --> Ans[Extracted / Generated Answer]
    
    %% Style Nodes
    classDef default fill:#1e1e2e,stroke:#cdd6f4,stroke-width:1px,color:#cdd6f4;
    classDef accent fill:#b4befe,stroke:#cdd6f4,stroke-width:2px,color:#11111b;
    class Ans accent;
```

---

## 🛠️ Key Challenges & Techniques

- **OCR Quality Dependency:** If the text recognition engine misidentifies figures or character symbols in small-font grids, the downstream reasoning layers cannot recover.
- **Complex Layout Parsing:** Document layouts often feature multiple columns, embedded tables, and footnotes, which challenge simple left-to-right reading orders.
- **Layout-Aware Embedding:** Utilizing 2D spatial embeddings to encode relative coordinates of words on the page, preserving document hierarchy.

# The Spatial Resolution Blur Bottleneck

Traditional Vision-Language Models (VLMs) downsample high-resolution images to a small fixed size (e.g., $224 \times 224$ or $336 \times 336$ pixels) to fit memory constraints, which blurs out crucial details like tiny text, serial numbers, barcodes, or small objects.

---

## 🏛️ AnyRes / Dynamic Resolution Partitioning

To preserve fine details, modern architectures deploy **Dynamic Resolution Patching (AnyRes / Megapixel Partitioning)**. High-resolution images are sliced into standard-size tiles matching the image's aspect ratio, plus a downsampled global thumbnail, and processed concurrently.

```mermaid
flowchart TD
    %% Define Nodes
    Img[High-Resolution Input Image] --> Split[Megapixel Partitioner / AnyRes]
    
    Split --> Tile1[Tile 1 - High Res]
    Split --> Tile2[Tile 2 - High Res]
    Split --> Global[Global Thumbnail - Low Res]
    
    Tile1 --> Enc[Shared Vision Encoder]
    Tile2 --> Enc
    Global --> Enc
    
    Enc --> Concat[Merged Visual Tokens]
    Concat --> LLM[Multimodal LLM Backbone]
    LLM --> Ans[Fine-Grained Detail Answer]
    
    %% Style Nodes
    classDef default fill:#1e1e2e,stroke:#cdd6f4,stroke-width:1px,color:#cdd6f4;
    classDef accent fill:#fab387,stroke:#cdd6f4,stroke-width:2px,color:#11111b;
    class Ans accent;
```

---

## 🛠️ Key Techniques & Adaptations

1. **LLaVA-NeXT AnyRes:** Slices images dynamically into aspect-ratio aligned grids (e.g., $1\times2$ or $2\times2$ tiles).
2. **NaViT (Native Resolution ViT):** Pack-and-patch sequence processing to avoid resizing and padding entirely by packing multiple resolutions directly into standard batch lengths.
3. **Token Pruning / Merging:** Removing redundant background tokens from tiles to reduce LLM attention calculation overhead.

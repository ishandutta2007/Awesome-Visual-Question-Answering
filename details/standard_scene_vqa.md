# Standard Scene VQA

**Standard Scene Visual Question Answering** targets natural, real-world photographs (e.g., indoor rooms, street layouts, outdoor landscapes). The questions typically evaluate the model's capacity for grounding objects, counting entities, describing traits, and identifying spatial relationships.

---

## 🏛️ Pipeline & Visual Grounding

The VQA core maps natural language question tokens to the spatial representations of objects detected inside a photographic scene. It resolves relative coordinates and spatial mappings to answer queries.

```mermaid
flowchart TD
    %% Define Nodes
    Img[Scene Photo] --> Det[Object Detector / segmentation]
    Det --> Objects[Object Regions & Coordinates]
    Que[Spatial Query<br/>e.g., 'What is next to the laptop?'] --> Core[Spatial Alignment Core]
    Objects --> Core
    Core --> Spatial[Relational Reasoning Grid]
    Spatial --> Ans[Grounded Text Answer]
    
    %% Style Nodes
    classDef default fill:#1e1e2e,stroke:#cdd6f4,stroke-width:1px,color:#cdd6f4;
    classDef accent fill:#f2cdcd,stroke:#cdd6f4,stroke-width:2px,color:#11111b;
    class Ans accent;
```

---

## 🛠️ Main Tasks

- **Attribute Recognition:** Identifying traits like colors, materials, and actions (e.g., `"What color is the shirt of the person riding the bicycle?"`).
- **Spatial Reasoning:** Mappings of absolute and relative positions (e.g., `"Is the coffee cup to the left of the keyboard?"`).
- **Counting:** Identifying the exact quantity of specific objects in cluttered scenes (e.g., `"How many cars are parked on the side of the road?"`).

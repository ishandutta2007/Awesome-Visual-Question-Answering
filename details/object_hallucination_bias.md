# Object Hallucination & Yes-Bias

Generative Vision-Language Models (VLMs) frequently hallucinate—asserting that objects exist in the scene when they are absent—due to strong language priors overriding visual visual cues. Models also suffer from **Yes-Bias**, answering "Yes" to leading questions.

---

## 🏛️ Evaluation & Mitigation Pipeline

We probe models using binary questions to detect hallucination rates, then align the VLM parameters using RLHF (Reinforcement Learning from Human Feedback) or DPO (Direct Preference Optimization) to penalize inaccurate assertions.

```mermaid
flowchart TD
    %% Define Nodes
    Img[Scene Image] & Que[Leading Question: 'Is there a cat?'] --> VLM[Standard VLM]
    VLM --> Hallucination{Hallucination Check<br/>POPE / Probing}
    
    Hallucination -->|Yes-Bias / False Pos| Align[Preference Optimization<br/>RLHF / DPO Alignment]
    Align --> Mitigated[Aligned VLM]
    
    Img & Que --> Mitigated
    Mitigated --> Correct[Corrected Answer: 'No, there is only a dog']
    
    %% Style Nodes
    classDef default fill:#1e1e2e,stroke:#cdd6f4,stroke-width:1px,color:#cdd6f4;
    classDef accent fill:#f38ba8,stroke:#cdd6f4,stroke-width:2px,color:#11111b;
    class Correct accent;
```

---

## 🛠️ Key Concepts & Mitigations

- **Object Hallucination:** Caused by visual-text misalignment or language models generating plausible sequences (e.g., hallucinating a laptop on an office desk because desks usually have laptops).
- **POPE (Polling-based Object Probing Evaluation):** Probing models with specific target objects (frequent, co-occurring, and random) using binary questions to extract clean precision/recall metrics.
- **DPO / RLHF:** Reinforcement training where the reward function penalizes answers that describe objects without corresponding coordinate regions in the image.

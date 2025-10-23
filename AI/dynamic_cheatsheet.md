# Dynamic Cheatsheet (DC): Test-Time Learning with Adaptive Memory

## Executive Summary

**Dynamic Cheatsheet (DC)** is a lightweight framework designed to equip large language models (LMs) with a **persistent, evolving memory** at inference time. Unlike traditional LMs that process each input query in isolation (*de novo*), DC enables models to store and reuse accumulated strategies, code snippets, and general problem-solving insights.

The framework enhances performance substantially across various challenging reasoning tasks without requiring explicit ground-truth labels, human feedback, or modification of the underlying model parameters (black-box compatibility).

**Key Performance Highlights:**

*   **Game of 24:** GPT-4o's success rate increased from approximately 10% (baseline) to **99%** under DC-RS after discovering and reusing a Python-based solution.
*   **AIME Math Exams:** Claude 3.5 Sonnet's accuracy more than **doubled** (e.g., 23.3% to 50.0% on AIME 2024 under DC-Cu) by retaining algebraic and combinatorial insights.
*   **Math Equation Balancer:** GPT-4o and Claude reached **near-perfect accuracy** (98–100%) by recalling previously validated code, significantly improving upon baseline performance (around 50%).
*   **Knowledge Tasks:** Claude achieved a 9% improvement in GPQA-Diamond and an 8% boost on MMLU-Pro Engineering and Physics problems.

---

## I. DC Framework and Methodology

DC establishes a flexible online-learning approach using an external, non-parametric memory that evolves alongside the LLM's inference process. This process involves two core, potentially shared, modules: *generation* and *curation*.

### A. Core Modules

1.  **Solution Generation (Gen):** At the $i$-th step, the generator produces a candidate solution ($\tilde{y}_i$) conditioned on the new query ($x_i$) and the current memory state ($M_i$). $M_i$ helps the model reuse or adapt previously stored solutions, techniques, or heuristics.
2.  **Memory Curation (Cur):** After generation, the curator updates the memory ($M_{i+1}$) based on the previous memory state, the query, and the candidate solution. The curator assesses the correctness and efficiency of solutions without access to ground-truth labels. Curation focuses on distilling the raw solution text into **succinct, generalizable, and high-impact references**.

### B. DC Variants

The research tested two primary variants of Dynamic Cheatsheet:

| Variant | Focus | Workflow | Key Features |
| :--- | :--- | :--- | :--- |
| **DC-Cu (Cumulative)** | Iterative accumulation | The system generates a solution and *then* updates the memory ($M_{i+1}$) by cumulatively expanding and refining the memory items. | **Does not include a retrieval component**. |
| **DC-RS (Retrieval & Synthesis)** | Retrieval-augmented refinement | Introduces a retrieval mechanism (*Retr*) and refines memory *before* generating a response. | Retrieval ($R_i$) finds the top-$k$ most similar past input-output pairs. The Curator updates memory ($M_i$) using $R_i$ and the current query, and *then* the Generator produces the solution ($\tilde{y}_i$). |

### C. Comparison to Baselines

DC variants were compared against several baselines:

*   **Baseline Prompting (BL):** Standard one-off inference with minimal guidance.
*   **DC-$\emptyset$ (Empty Memory):** A stronger baseline using explicit structured instructions (e.g., for Python code generation), but lacking a memory retention mechanism.
*   **Dynamic Retrieval (DR):** Retrieves the most similar past interactions *verbatim* but lacks memory curation or generalization.
*   **Full-History Appending (FH):** A naive approach that appends the entire conversation history without curation or truncation.

DC's **selective memory curation** makes it more robust than FH, which often results in context ballooning, dilution of insights, and worse performance (e.g., GPT-4o's AIME 2024 score *dropped* from 20.0% to 6.7% using FH). DC also demonstrated superior performance over **Majority Voting (MV)**, which passively aggregates outputs, whereas DC actively refines knowledge over time.

---

## II. Insights and Implications

### A. Fostering Efficient Tool Usage

A major success of the DC framework is the LLMs' inclination toward efficient tool usage and code generation for computationally intensive tasks.

*   In Game of 24, GPT-4o recognized that a **Python-based brute-force solver** was more systematic than manual arithmetic. Once this script was generated, stored, and iteratively refined, the model retrieved and applied it consistently, eliminating arithmetic errors and leading to near-perfect accuracy.
*   This inclination suggests DC can nurture the capacity to recognize when external tools (like Python interpreters) are more robust than internal verbalized calculations, spreading this computational benefit across multiple interactions.

### B. Impact of Model Scale and Generative Competence

The effectiveness of DC is highly dependent on the base model's scale and underlying generative capacity.

*   **Larger Models (e.g., GPT-4o, Claude 3.5 Sonnet)** showed notable gains, as they produced correct solutions frequently enough to populate the memory with high-quality, reusable strategies.
*   **Smaller Models (e.g., GPT-4o-mini, Claude 3.5 Haiku)** showed limited or inconsistent gains. They struggle because:
    1.  They generate fewer correct solutions, leading to a sparse or low-quality memory repository where stored knowledge consists mostly of incorrect attempts.
    2.  They struggle with contextual understanding and memory retrieval, often failing to retrieve the most relevant past solutions or misapplying retrieved knowledge.

### C. Learning Dynamics and Efficiency

*   **Curriculum-Style Learning:** DC performs best when sequential test examples share structural similarities (e.g., Game of 24 instances). This suggests that arranging tasks to present related questions early may accelerate test-time learning by allowing the model to quickly build a repository of valid heuristics.
*   **Reduced Overhead:** By reusing established techniques (e.g., Python scripts), DC reduces the need to "reinvent the wheel" for each query, significantly cutting down reasoning overhead and token usage in subsequent queries, though the initial cost of discovering a robust approach and curating it remains non-trivial.
*   **Retrieval Noise:** While retrieval (DC-RS) boosts accuracy, poorly filtered retrieval can introduce confusion, particularly if suboptimal examples are recalled. This was observed when GPT-4o’s performance dipped occasionally in GPQA-Diamond, underscoring the importance of robust retrieval methods.

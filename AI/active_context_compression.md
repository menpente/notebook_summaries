https://arxiv.org/html/2601.07190v1

# Briefing Document: Active Context Compression (Focus Agent)

### **Executive Summary**
This document outlines the **Focus** architecture, an agent-centric memory management system designed to mitigate **"Context Bloat"** in Large Language Model (LLM) agents. Inspired by the biological exploration strategies of *Physarum polycephalum* (slime mold), the Focus Agent **autonomously decides when to consolidate key learnings** into a persistent Knowledge block while **actively pruning raw interaction history**. Testing on SWE-bench Lite demonstrated a **22.7% reduction in token usage** while maintaining identical task accuracy (60%) compared to baseline agents.

---

### **The Problem: Context Bloat**
While modern LLMs support massive context windows, utilizing them naively leads to three primary failures:
*   **Cost:** Re-processing growing histories at every inference step creates **quadratic cost accumulation**.
*   **Latency:** Increased context length results in **sluggish time-to-first-token** performance.
*   **Context Poisoning:** Redundant trial-and-error logs and verbose tool outputs can distract the model, a phenomenon known as being **"Lost in the Middle"**.

---

### **The Solution: Focus Architecture**
The Focus architecture shifts from **"Passive Retention"** (append-only logs) to **"Active Compression"**. It introduces two autonomous primitives to the agent loop:

1.  **`start_focus`:** The agent declares a sub-task (e.g., "Debug database connection"), creating a **checkpoint** in the conversation history.
2.  **`complete_focus`:** Upon finishing the sub-task or hitting a dead end, the agent generates a summary of attempts, findings, and outcomes.

**The "Withdraw" Mechanism:**
The system appends the agent's summary to a **persistent "Knowledge" block** at the top of the context window and **deletes all raw messages** between the checkpoint and the current step. This creates a **"Sawtooth" pattern** of context growth and collapse, preventing the monotonically increasing log seen in standard agents.

---

### **Key Performance Metrics**
Evaluated using **Claude Haiku 4.5** on context-intensive software engineering tasks (N=5), the results show:

| Metric | Baseline Agent | Focus Agent | Delta |
| :--- | :--- | :--- | :--- |
| **Total Tokens** | 14.9M | 11.5M | **-22.7%** |
| **Task Success** | 3/5 (60%) | 3/5 (60%) | **Same** |
| **Avg. Compressions** | 0 | 6.0 | -- |
| **Avg. Messages Dropped**| 0 | 70.2 | -- |

**Instance-Specific Savings:**
*   **Maximum Savings:** Tasks requiring extensive codebase navigation, such as `matplotlib-26020` and `sympy-21171`, saw token reductions of **57%**.
*   **Overhead Risk:** Tasks requiring iterative refinement (e.g., `pylint-7080`) showed a **110% increase** in token usage because frequent pruning forced the agent into redundant re-exploration.

---

### **Critical Success Factors**
The research highlights that **aggressive prompting** is essential for effective context management:
*   **Frequency Matters:** Passive prompting resulted in only 6% savings and accuracy loss.
*   **Instructional Guardrails:** Agents must be explicitly commanded to **"ALWAYS call complete_focus after 10-15 tool calls"** and receive periodic system reminders.
*   **Structured Phases:** Guiding the agent through explicit phases (Explore $\rightarrow$ Understand $\rightarrow$ Implement $\rightarrow$ Verify) ensures compressions happen at logical task boundaries.

---

### **Strategic Insights and Limitations**
*   **Exploration vs. Iteration:** Focus is most valuable for **exploration-heavy tasks** where it can discard verbose directory listings and failed attempts while preserving the "learned map".
*   **Cognitive Tax:** Generating summaries and managing focus phases introduces a "tax" that is only amortized over longer tasks (50+ tool calls).
*   **Infrastructure-Free:** Focus operates entirely within the conversation history, requiring no external summarization models or complex memory hierarchies.
*   **Future Work:** Key areas for development include **fine-tuning** for intrinsic cost-awareness and validating the approach on larger datasets like the full SWE-bench (N=300).

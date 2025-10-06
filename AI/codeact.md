## Briefing Document: Executable Code Actions Elicit Better LLM Agents (CodeAct)

This briefing summarizes the key findings and methodology of a proposed framework, CodeAct, designed to enhance Large Language Model (LLM) agents by utilizing executable Python code for actions.

---

### I. Core Problem and Proposed Solution

**The Challenge with Traditional LLM Actions:**
LLM agents are typically prompted to generate actions using JSON or text in a pre-defined format, often for tasks like invoking tools or controlling robots. These methods suffer from several limitations:
1.  **Constrained Action Space:** Actions are usually tailored for specific tasks.
2.  **Restricted Flexibility:** There is often an inability to compose multiple tools within a single action.
3.  **Data Requirements:** JSON or specialized text formats require specific data curation efforts for fine-tuning.

**CodeAct: Executable Python Code as a Unified Action Space:**
The research proposes **CodeAct**, a general-purpose framework where LLMs generate **executable Python code as actions**. This approach consolidates LLM agents’ actions into a unified action space. Python was chosen due to its popularity and the numerous open-source packages available.

### II. Advantages of Using Code Actions

CodeAct offers unique benefits over text or JSON actions, particularly for complex tasks:

| Advantage | Description | Sources |
| :--- | :--- | :--- |
| **Dynamic Interaction & Self-Debugging** | Integrated with a Python interpreter, CodeAct can **execute code actions** and dynamically revise previous actions or emit new actions based on environmental observations (e.g., execution results or errors) through **multi-turn interactions**. This enables autonomous error rectification via self-debugging using automated feedback like tracebacks. | |
| **Expanded Action Space (Tool Use)** | Code actions allow LLMs to directly leverage **existing software packages** (e.g., Python packages available on PyPI) instead of requiring human effort to curate tools from scratch. | |
| **Complex Logical Operations** | Code inherently supports **control and data flow** (e.g., `if`-statements, `for`-loops), enabling the storage of intermediate results and the composition of multiple tools to perform complex logical operations with a single piece of code. Traditional formats require careful engineering to mimic such logic. | |
| **Cost-Effective Adoption** | LLMs are generally familiar with structured programming languages because code data is widely used in pre-training. This familiarity makes CodeAct a better optimization route for open-source LLMs. | |

### III. Empirical Evidence (Quantitative Results)

Experiments were conducted on 17 LLMs using three action modes: CodeAct, JSON, and Text.

#### A. Complex Tool Use (M3ToolEval)
M3ToolEval is a new benchmark featuring 82 human-curated tasks requiring intricate coordination and composition of multiple tools in multi-turn interactions.

*   **Success Rate:** CodeAct achieved higher success rates for 12 out of 17 evaluated LLMs.
*   **Efficiency:** CodeAct generally required a **lower average number of interaction turns** (12 out of 17 LLMs).
*   **Peak Performance:** The best model, `gpt-4-1106-preview`, achieved up to a **20.7% absolute improvement** over the next best action format (Text) while requiring 2.1 fewer turns on average.

#### B. Atomic Tool Use (API-Bank)
On basic tasks involving only atomic tool use, CodeAct achieved comparable or better performance than JSON and Text, demonstrating its advantage even when control and data flow features are ablated.

### IV. CodeActAgent and CodeActInstruct

The success of CodeAct motivated the creation of an open-source LLM agent.

#### A. CodeActAgent
**CodeActAgent** is an open-source LLM agent fine-tuned from Llama-2 and Mistral, specifically designed for seamless integration with Python. It is capable of performing sophisticated tasks (e.g., model training, data visualization using packages like Pandas, Scikit-Learn, and Matplotlib) and autonomously self-debugging.

#### B. CodeActInstruct Dataset
**CodeActInstruct** is an instruction-tuning dataset containing 7,139 high-quality, multi-turn interaction trajectories using CodeAct. It focuses on agent-environment interactions and was generated using stronger LLMs like GPT-4 and Claude.

The dataset covers diverse domains:
*   **Information Seeking:** Using search APIs (HotpotQA).
*   **Software Package Usage:** Math reasoning (MATH) and code generation (APPS).
*   **External Memory:** Tabular reasoning using SQL (`sqlite3`) or Pandas.
*   **Robot Planning:** Interacting with embodied environments (ALFWorld).

Crucially, the dataset selection process specifically preserved trajectories where the model initially encountered errors but subsequently rectified those inaccuracies in later interactions, thereby promoting the agent’s self-improving and self-debugging capabilities.

#### C. Performance of CodeActAgent
CodeActAgent (Mistral variant) outperformed all evaluated open-source LLMs on CodeAct agent tasks (MINT in-domain, MINT out-of-domain, and M3ToolEval). Furthermore, it maintained or improved performance on a suite of generic LLM tasks (MMLU, HumanEval, GSM8K, MTBench).

*Note on Llama-2 Anomaly:* The Llama-2 variant of CodeActAgent failed to improve performance on M3ToolEval, potentially due to pre-training artifacts or the LLaMA-2 backbone’s weaker fundamental capability compared to Mistral.

### V. Societal Impact and Safety Concerns

CodeActAgent, while demonstrating limited self-improving capabilities, is an initial prototype. Potential risks are associated with granting the agent the ability to freely execute code in a sandbox environment. In a worst-case scenario, such an agent could potentially break free and cause harm (e.g., through a cyber-attack), underscoring the necessity of designing better safety mechanisms for autonomous agents.

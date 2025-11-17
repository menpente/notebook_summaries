# Briefing Document: The Era of Agentic Organization and Asynchronous Thinking (AsyncThink)

## 1. Vision: The Era of Agentic Organization

The next era of artificial intelligence is defined by the concept of **agentic organization**, where multiple AI agents form organized systems that collaborate concurrently to solve complex problems, achieving outcomes beyond the limits of individual intelligence.

This vision is motivated by the fact that while large language models (LLMs) have remarkable reasoning capabilities as individual agents, complex tasks require organized, collaborative reasoning.

### Challenges in Agentic Organization
1.  **Latency:** Organizing agents concurrently often incurs additional latency. Current parallel thinking methods are limited by the slowest trace and the delay incurred during final outcome aggregation.
2.  **Adaptivity and Dynamism:** Existing parallel thinking relies on manually designed, fixed workflows that cannot adapt to the diverse requirements of different queries (e.g., some need divide-and-conquer, others need step-by-step reasoning).
3.  **Policy Learning:** Manually designing optimal thinking structures for every query is intractable, making learning effective organization policies an open problem.

## 2. Asynchronous Thinking (AsyncThink) Paradigm

**AsyncThink** is introduced as a new reasoning paradigm designed to learn to organize the internal thinking of LLMs into **concurrently executable structures**.

### Comparison to Existing Paradigms
*   **Sequential Thinking:** Employs a purely sequential decoding trajectory (realized when AsyncThink takes no Fork actions).
*   **Parallel Thinking:** Executes multiple independent traces with an outcome aggregation (realized when the organizer repeatedly assigns the original query to multiple workers).
*   **AsyncThink:** Learns to form an agentic organization to think concurrently and collaboratively. It dynamically structures the process through **Fork** and **Join** actions.

## 3. The Organizer-Worker Thinking Protocol

The AsyncThink approach utilizes an **organizer-worker thinking protocol**, where a single LLM backbone plays both roles, performing autoregressive text decoding.

### Roles and Actions
| Role | Responsibility | Key Actions | Details & Format |
| :--- | :--- | :--- | :--- |
| **Organizer** | Global coordination and managing the thinking processes. Receives the initial user query and drives the entire thinking process. | **Think** | Advances the current decoding process in its own thread. |
| | | **Fork** | Assigns a sub-query job to an available worker. Format: `〈FORK-i〉 sub-query 〈/FORK-i〉`. Cannot Fork if sub-query `i` exists or if $c-1$ active workers are running. |
| | | **Join** | Requests the output of a previously Fork-ed job (`〈JOIN-i〉`). If the worker is running, the organizer pauses until the worker returns results, which are then appended to the organizer's decoding context. |
| | | **Answer** | Terminates the inference process and produces the final answer. |
| **Worker** | Executes individual thinking processes for assigned sub-queries within an agent pool of capacity $c$ (meaning $c-1$ workers). | **Return** | Sends results back to the organizer. Format: `... thoughts ... 〈RETURN〉 some takeaways〈/RETURN〉 ...`. |

This protocol uses Fork and Join actions to control the trajectory of thinking and provides the foundation for adaptivity and dynamic reasoning.

## 4. Training Methodology

AsyncThink is trained using a **two-stage procedure** to acquire the ability to organize thinking.

### Stage 1: Cold-Start Format Fine-Tuning (SFT)
*   **Purpose:** To teach the model the syntax and format of AsyncThink actions.
*   **Data Synthesis:** Training data (organizer-worker thinking traces) is synthesized using models like GPT-4o, which analyzes the query to detect conditionally independent thinking fragments.
*   **Randomization:** To prevent the model from collapsing into fixed thinking topologies (like interleaved Fork/Join or pure parallel Fork-then-Join patterns), randomly sampled organizer action sequences are added to the prompt to guide the model, enabling broader exploration during the subsequent stage.

### Stage 2: Reinforcement Learning (RL)
The SFT stage only teaches syntax; RL is used to optimize the model to exploit the thinking mechanism and produce correct answers. The policy optimization extends Group Relative Policy Optimization (GRPO).

**Rule-Based Reward System:** Rewards encourage correctness and efficiency.

1.  **Accuracy Reward ($R_A$):** Measures the accuracy of final answers (e.g., binary reward for single-answer questions or proportional reward for multi-solution tasks).
2.  **Format Reward ($R_{FE}$):** Penalizes specific format errors, such as duplicated sub-query indices, agent pool overflow (forking when $c-1$ workers are active), joining a non-existing sub-query, or stopping without generating a final answer.
3.  **Thinking Concurrency Reward ($R_\eta$):** Encourages efficiently organizing processes into concurrently executable parts. This reward is based on the thinking concurrency ratio ($\eta$), which is the average number of active workers ($a_t$) over the total critical-path latency ($T$). Removing this reward leads to reduced accuracy and higher latency.

## 5. Evaluation and Key Results

AsyncThink consistently demonstrates improved accuracy and reduced latency across reasoning tasks.

### Evaluation Metrics
1.  **Final-Answer Accuracy:** Measures the correctness of the final answers.
2.  **Critical-Path Latency:** Measures the minimum sequential depth required for asynchronous thinking. This represents a theoretical lower bound on inference time, computed using a dynamic programming method across organizer fragments and worker thinking times.

### Performance Highlights
*   **Efficiency:** AsyncThink achieves **28% lower inference latency** compared to parallel thinking while simultaneously improving accuracy on mathematical reasoning tasks.
*   **Multi-Solution Countdown (MCD):** AsyncThink substantially outperformed sequential and parallel thinking, achieving 89.0% accuracy on the strict 'All Correct' metric, compared to 68.6% and 70.5% for baselines, showing enhanced multi-solution coverage.
*   **Math Reasoning (AIME-24 and AMC-23):** AsyncThink achieved the best overall performance with substantially lower critical-path latency compared to baselines (e.g., 1468.0 latency on AIME-24 compared to 2048.0 for Parallel-Thinking-L2K). The results suggest that short, organized thinking fragments can collectively achieve high problem-solving quality under the learned organization policy.
*   **Generalization to Unseen Tasks:** AsyncThink models demonstrated strong zero-shot generalization of asynchronous thinking capabilities to previously unseen tasks, such as the 4x4 Sudoku task, even when trained solely on simple countdown data. On Sudoku, AsyncThink achieved 89.4% accuracy compared to 84.2% for Parallel-Thinking, while maintaining lower latency.

## 6. Future Directions

Future research focuses on expanding the power and scope of agentic organization:

*   **Scaling Agentic Organization:** Exploring how accuracy and latency trade-offs evolve as the agent pool capacity grows and transitioning from a homogeneous pool to a massive organization of heterogeneous expert workers equipped with different external tools.
*   **Recursive Agentic Organization:** Enabling any worker to dynamically be promoted to a sub-organizer, allowing it to Fork its own team of sub-workers. This creates a flexible, hierarchical structure suited for deeply nested and complex problems.
*   **Human-AI Agentic Organization:** Integrating humans directly into the organization, either as a "Human-as-Organizer" dispatching tasks to AI workers, or a "Human-as-Worker" where the AI Forks tasks requiring human judgment.

***
*Analogy: AsyncThink functions much like a dynamic construction site manager. Sequential thinking is one worker doing every task alone, step-by-step. Parallel thinking is four independent workers building four separate mini-structures and hoping they fit together at the end. AsyncThink, however, is a manager who breaks down the blueprint (query) into specialized tasks (sub-queries), sends them to available skilled workers (concurrent workers), and crucially, pauses its own work to wait for specific results (Join) before merging that intermediate knowledge and deciding the next step (Fork or Answer), resulting in faster, more organized, and ultimately higher-quality construction.*

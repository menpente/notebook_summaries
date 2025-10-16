## DSPy: Compiling Declarative Language Model Calls into Self-Improving Pipelines

This briefing document outlines the DSPy programming model, its core abstractions, the compilation process, and empirical results demonstrating its effectiveness in developing high-quality Language Model (LM) pipelines without reliance on manual prompt engineering.

### 1. Introduction and Motivation

The development of sophisticated LM pipelines typically involves implementing LM calls using **hard-coded ‘prompt templates’**, which are lengthy strings discovered through manual trial and error. This approach is often brittle and unscalable, conceptually similar to hand-tuning the weights of a classifier.

**DSPy** (pronounced dee-ess-pie) is introduced as a programming model to overcome these challenges, offering a more systematic approach to designing AI pipelines. DSPy abstracts LM pipelines as **text transformation graphs**—imperative computation graphs where LMs are invoked through declarative modules. DSPy pushes development away from manipulating free-form strings and closer to programming, allowing a compiler to automatically generate optimized LM invocation strategies and prompts from a program.

### 2. Core DSPy Abstractions

DSPy contributes three key abstractions toward automatic optimization: **signatures**, **modules**, and **teleprompters**.

#### 2.1 Natural Language Signatures

DSPy programs use **natural language signatures** to assign work to the LM, replacing free-form string prompts. A signature is a natural-language typed declaration of a function—a short declarative specification defining **what** a text transformation must do (e.g., "consume questions and return answers"), rather than *how* an LM should be prompted.

A DSPy signature is formally a tuple of input fields and output fields (plus an optional instruction). In practice, this can be expressed using shorthand notation, such as `question -> answer`.

**Benefits of Signatures:**
1.  They can be compiled into **self-improving and pipeline-adaptive prompts** or finetunes.
2.  They handle structured formatting and parsing logic, reducing reliance on brittle string manipulation in user programs.

#### 2.2 Parameterized Modules

**Modules** are task-adaptive components, akin to neural network layers, that abstract any specific text transformation. They are designed to translate prompting techniques (like Chain of Thought or ReAct) into modular functions that support any signature.

*   **Parameterization:** DSPy uniquely **parameterizes** these prompting techniques. These parameters include the specific LM to call, field prefixes, and, most importantly, the **demonstrations** used for few-shot prompting or training data.
*   **Module Composition:** Modules are composed in arbitrary pipelines using a **define-by-run interface**, inspired by PyTorch.
*   **Key Modules:**
    *   **Predict:** The core module for working with signatures, storing the signature, an optional LM, and a list of demonstrations.
    *   **ChainOfThought (CoT) / ReAct:** Sophisticated built-in modules that generalize existing reasoning techniques. These modules expand the user-defined signature and call `Predict` one or more times on new signatures (e.g., adding a `rationale` output field to the signature for CoT).
    *   **dspy.Retrieve:** Supports tools such as retrieval models, with built-in support for systems like ColBERTv2.

For example, a Retrieval-Augmented Generation (RAG) system can be expressed concisely by declaring and composing `dspy.Retrieve` and `dspy.ChainOfThought` modules.

#### 2.3 Teleprompters and Optimization

A **teleprompter** is the optimizer in DSPy, automating the task of prompting without manual intervention. When compiling a DSPy program, the teleprompter takes the program, a training set (which may be small and incomplete, often only requiring labels for the final output), and a metric.

The optimization goal is to improve the quality or cost of modules via prompting or finetuning, which DSPy unifies.

The DSPy compiler generally follows three stages:

1.  **Candidate Generation:** Finds unique `Predict` modules and generates candidate values for their parameters, focusing on demonstrations. For example, the `BootstrapFewShot` teleprompter simulates a teacher program (or a zero-shot version) on training inputs, collecting **multi-stage traces**.
2.  **Parameter Optimization:** Uses the program’s metric to filter for traces that lead to valid output. These "good examples" are used as potential demonstrations, which can then be optimized using methods like random search (e.g., `BootstrapFewShotWithRandomSearch`) or finetuning (`BootstrapFinetune`).
3.  **Higher-Order Program Optimization:** Modifies the control flow, such as creating **ensembles** that run multiple copies of a program in parallel and combine their predictions (e.g., via majority voting).

### 3. Comparison with Existing Libraries

Existing toolkits, such as **LangChain** and **LlamaIndex**, generally provide pre-packaged components and chains, but they **suffer internally from the prompt engineering challenges that DSPy aims to resolve**. These libraries express task-specific behavior through manually hand-written prompt templates.

In contrast, DSPy introduces core composable operators (signatures, modules, teleprompters) and focuses on automatic compilation.

*   An informal study showed that in late September 2023, the LangChain codebase contained 50 strings exceeding 1000 characters, generally representing prompts.
*   DSPy provides a structured framework that automatically bootstraps prompts, and the library itself **does not contain a single hand-written prompt demonstration for any tasks**.
*   Examples of extensive prompt engineering in existing libraries include the LangChain Program-Aided Language Model chain program, which uses a template that is 3,982 characters long.

### 4. Empirical Success

DSPy was tested using diverse tasks to evaluate three hypotheses: (H1) DSPy can replace hand-crafted prompts without reducing quality, (H2) Parameterizing modules improves adaptation across LMs and may outperform expert prompts, and (H3) Modularity allows for thorough exploration of complex pipelines.

#### 4.1 Case Study: Math Word Problems (GSM8K)

On the GSM8K dataset, compiling DSPy programs with the bootstrap procedure led to large gains across different programs and LMs. The programs tested included `vanilla` (Predict), `CoT` (ChainOfThought), and `reflection` (using `MultiChainComparison`).

**Key Findings:**
*   Compiling the correct generic modules, instead of relying on string prompts, improved different LMs from **4–20% accuracy to 49–88% accuracy**.
*   For the CoT program, DSPy's **bootstrap** approach could **match or surpass** performance achieved using expert human reasoning chains (+human CoT).
*   The `reflection` program, which samples five reasoning chains and compares them, was a clear winner when optimized.
*   Llama2-13b-chat compiled with DSPy programs became competitive with results previously reported for models like PaLM 540-B and even Llama2-34b.

#### 4.2 Case Study: Complex Question Answering (HotPotQA)

This case study explored multi-hop retrieval question answering. Programs included RAG (using retrieval and CoT), ReAct (a multi-step agent module), and a custom `BasicMultiHop` program.

**Key Findings:**
*   The `multihop` program, which iteratively generates search queries for retrieval in two hops, performed the best when compiled.
*   The **bootstrap** compiler proved very effective at raising the quality of the `multihop` program relative to its `fewshot` variant for both GPT-3.5 and llama2-13b-chat.
*   DSPy enabled **llama2-13b-chat to become competitive with GPT-3.5** simply by compiling the programs.
*   A **T5-Large (770M parameter) model**, compiled using `BootstrapFinetune` with a teacher program, scored 39.3% answer EM, demonstrating that DSPy allows the use of relatively small and efficient LMs effectively. This compiled program imposed orders of magnitude lower costs for inference than proprietary LMs like GPT-3.5.

### 5. Conclusion

DSPy offers a new programming model that allows for the rapid development of highly effective AI systems using pipelines of pretrained LMs. By introducing **declarative signatures**, **parameterized modules**, and **general-purpose optimizers (teleprompters)**, DSPy enables the construction of sophisticated text transformation graphs that leverage LMs in more systematic and reliable ways, minimizing or eliminating the role of artful, hand-crafted prompt construction.

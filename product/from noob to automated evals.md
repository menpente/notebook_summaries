# Briefing Document: From Noob to Automated Evals In A Week (as a PM) with Teresa Torres

This briefing document summarizes Teresa Torres's journey from a product management expert with limited AI engineering experience to developing a sophisticated AI-powered "Interview Coach" and establishing a robust evaluation workflow for her product. Her insights highlight the practical application of AI, the importance of iterative development, and the crucial role of domain expertise in building effective AI products.

## 1. Introduction: Teresa Torres's Background and AI Journey

Teresa Torres is a renowned figure in product management, author of "Continuous Discovery Habits," and an educator who has trained over 70,000 people. With a background in product discovery coaching, her primary work is helping product teams make better decisions. Despite not coding daily, she embarked on building an AI product driven by the question: **"What does generative AI make just now possible?"**. This journey started in March, with minimal prior knowledge of AI evaluations (evals).

## 2. The Product: The Interview Coach

The AI product Teresa built is an "Interview Coach" designed for her continuous interviewing course. In this course, students learn specific customer interviewing techniques, focusing on asking story-based questions, active listening, and eliciting specific past behaviors for reliable feedback. The core problem the coach addresses is providing expert feedback, as students giving feedback to each other are not experts.

**How the Interview Coach Works:**
*   Students submit interview transcripts.
*   The coach provides detailed feedback on their interview performance.
*   It evaluates transcripts across four key dimensions based on the course rubric:
    *   **Asking story-based questions:** Did the interviewer ask the participant to share a specific story?
    *   **Setting the scene:** Did they prompt the participant to describe the context, aiding memory recall?
    *   **Building the timeline:** Did they help the participant go step-by-step through their story to understand what happened?
    *   **Redirecting generalizations:** Did they guide the participant back to specific details when they started generalizing?
*   For each dimension, the coach provides a score (e.g., "keep practicing," "getting it," or "great"), pulls out real excerpts from the transcript, and offers a tip for improvement.

**Evolution of the Coach's Design:**
*   The initial prototype was built in Claude, uploading instructional content and the evaluation rubric.
*   It started as one prompt but evolved into a complex workflow involving **five to nine LLM calls** depending on content and context.
*   Teresa envisions it becoming an "agent model" that adjusts feedback based on a student's learning history.

## 3. The Challenge: Evaluating AI Output and Establishing a Feedback Loop

Initially, Teresa "vibe checked" the coach's responses, noticing some were good and some had problems, leading to concerns about its quality. Her product discovery expertise, which emphasizes feedback loops, prompted her to seek a more systematic way to evaluate the AI. She found initial information on evals overwhelming, especially concerning the need for large input data sets, which she lacked.

## 4. Solution: The Evals Journey

Teresa's approach to evaluations was heavily influenced by a class she took, where the concept of evals as the "scientific method" resonated with her.

### 4.1. Initial Setup and Data Collection
*   **AirTable for Traces and Annotations**: Leveraging a familiar tool, she stored "traces" (interview transcripts and coach responses) in AirTable and used its interface as her first annotation tool.
*   **Small Data Sets**: Her initial dataset comprised about 15 interviews she conducted, 10 from instructors, and 10 from alumni.
*   **Identifying Failure Modes**: Her first annotation round revealed numerous failure modes, leading her to realize her coach "sucked," despite her initial positive "vibe check".

### 4.2. Developing Evals with Jupyter Notebooks
*   **Coding Background**: While not a daily engineer, Teresa has a computer science background, front-end development experience, and recently started coding again for business automation. She chose AWS's serverless environment (Node.js Lambda functions orchestrated with Step Functions) to avoid managing infrastructure.
*   **Jupyter Notebooks**: Introduced to Jupyter notebooks by her husband, she used Chat GPT to learn how to use them as a total beginner.
    *   Notebooks allowed her to brainstorm eval ideas in Markdown, then implement and execute them in code cells, comparing different approaches.
*   **First Evals: Leading and General Questions**:
    *   **Leading Question Eval (LLM as Judge)**: This eval prompts an LLM to identify if suggested follow-up questions are leading (implying an answer). Teresa iterated heavily on strategies to align this LLM-as-judge eval with human labels.
    *   **General Question Eval (Code Assertion)**: She discovered that general questions could be identified by a small set of "red flag" keywords, allowing for a highly accurate code assertion eval. This demonstrated the value of **domain expertise** in identifying simple, effective eval strategies that an engineer might miss.

### 4.3. Efficiency and Data Analysis
*   **Helper Functions (Context Engineering)**: Teresa developed helper functions to pre-process interview transcripts and extract only the relevant information (e.g., coaching tips, suggested questions) for the evals. This drastically reduced input token size for LLM calls, saving money and making evals faster. This is referred to as "context engineering".
*   **Notebook as a Data Analysis Tool**: She used Chat GPT to transform her notebook into a data analysis tool, allowing her to:
    *   Run multiple evals against her traces.
    *   Visualize results (e.g., frequency of failure modes).
    *   Investigate individual failures, compare human labels to eval labels, and identify bugs in helper functions or even flaws in her human labeling rubric.

### 4.4. Fast Feedback Loops and Iteration
*   **Measuring Impact**: The evals provided a structured way to measure the impact of changes (model, prompt, temperature, chunking, workflow).
*   **Continuous Improvement**: By running evals on development sets, she could quickly see which evals improved or worsened, enabling informed judgment calls on whether to release changes. This "fast feedback loop" was described as "magical" for measuring a non-deterministic product.

## 5. Evolution of the Workflow and Production Readiness

Teresa's workflow matured significantly throughout the project, moving from initial experimentation to a production-ready system.

*   **VS Code and Claude Code**: She transitioned to VS Code and heavily utilizes Claude Code for **pair programming**. She emphasizes the importance of understanding every line of generated code to ensure maintainability, rather than just "vibe coding".
*   **Advanced Notebook Features**: Her current notebook acts as a powerful diagnostic tool, allowing her to select a transcript and see what helper functions extracted and what each eval returned. She even created custom widgets in notebooks with Claude Code's help.
*   **Separation of Concerns**: Eval code is now part of her main repository and runs as production guardrails, while the notebook serves primarily as a data analysis and diagnostic tool.
*   **Custom Annotation Tools**: Claude Code built her custom annotation tools, which are highly visual, color-coded, and support fast keyboard shortcuts. These tools can be quickly adapted for different annotation needs.
*   **Production Launch with Vistily**: The interview coach is being rolled out as a beta feature within Vistily, a product discovery software company. This partnership addresses the need for secure, compliant data handling, as students were submitting sensitive customer data. This transition required her to learn "real software engineering" practices, including robust error handling, often by collaborating with LLMs.

## 6. Key Insights and Takeaways

*   **LLMs as Guides and Thought Partners**: Teresa credits LLMs (Chat GPT, Claude, Opus, Sonnet) as critical "thought partners" that helped her learn, get unstuck, and re-architect complex systems. She advises asking "dumb questions" without embarrassment and iterating through conversations.
*   **Importance of Understanding Code**: Despite using LLMs to generate code, her philosophy is to understand every line to prevent unmaintainable products.
*   **Domain Expertise is Crucial for Evals**: Her ability to identify simple yet effective eval strategies (like the keyword-based general question eval) stemmed directly from her deep teaching experience. This highlights the need for close collaboration between domain experts (like product managers) and engineers in AI product development.
*   **Iterative Problem Solving and Learning**: The process involves identifying the smallest piece to learn, working with LLMs, and iterating. She emphasizes taking breaks to gain fresh perspectives on problems.
*   **Value of Problem-Solving Skills**: Her computer science and symbolic systems background fostered critical thinking and problem-solving skills, which she believes are highly transferable and beneficial in this new AI landscape.
*   **Measuring Before Fixing**: A core principle she applies from product discovery to AI engineering is to measure the problem (e.g., 81% error rate) before implementing fixes, and then measure again (e.g., 3% error rate) to confirm improvement.

## 7. Future Outlook

Teresa is actively contemplating how product managers, designers, and engineers will collaborate in this new AI paradigm. She suggests that notebooks could help by abstracting some code while still allowing analysis and visualization. She is also launching a podcast to interview cross-functional product teams about how they're building AI products, focusing on "who did what and how do we collaborate". She aims to create a light, freely available version of the coach based on the leading and general question evals.

## 8. Follow-Up

Teresa Torres shares her insights on her blog at producttalk.org and on LinkedIn and X (formerly Twitter).

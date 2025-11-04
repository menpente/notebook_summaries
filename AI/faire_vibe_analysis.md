https://youtu.be/KOr-xQuNK4A

# AI-Powered Data and Product Analysis at Faire: A Briefing Document

This briefing summarizes the implementation and impact of new AI tools, such as Cursor, Enterprise Search, and custom agents, used by Faire's data team to revolutionize product analysis, often referred to as "Vibe analysis". These tools have transformed the typically hours-long process of gathering context into minutes, allowing for quicker and much better analysis.

## I. Foundational Concepts and Tools

The analytical workflows detailed rely heavily on three key components:

### Context Gathering and AI Search
The most crucial—and often most difficult—part of analysis is gathering the right context and knowing which questions to ask.

*   **Enterprise AI Search:** Tools like Notion AI (used at Faire) allow self-service searching across diverse systems like Slack, Notion, Jira, and GitHub. This enables analysts to quickly delve into unfamiliar topics.
*   **Cursor:** Used for writing, creating, and editing SQL, described as "gamechanging". It functions as an "ultimate context engine" due to its ability to hook up to various business systems.

### Model Context Protocols (MCPs)
MCPs allow AI models to connect programmatically to various applications. These are crucial for eliminating context switching, copying, and pasting, enabling the models to perform tasks directly.

*   **Examples of MCP Connections:** Snowflake (data warehouse), Notion (documentation), Mode (BI tool), EPO (experimentation tool). While powerful and seemingly magical, setting up MCPs requires significant work from data engineering.

### Semantic Layer
This concept defines a structured translation for a Large Language Model (LLM) encompassing business terms, tables, fields, filters, and metrics.

*   **Benefits:** It democratizes data, enabling anyone in the company to self-serve answers to basic questions (e.g., average order size). For deeper analysis, specialized semantic layers can be built and managed by code within the data science repository, increasing the zero-shot ability of running accurate SQL queries.

## II. Key Analytical Workflows

The sources demonstrate four core use cases for leveraging AI in data analysis:

### 1. Incident Investigation and Root Cause Analysis

This workflow addresses sudden drops in critical metrics, such as the new customer conversion funnel.

| Step | Technique/Tool Used | Insight/Result |
| :--- | :--- | :--- |
| **Initial Hypothesis Generation** | Enterprise AI Search (Notion) | Asking for new features or experiments launched within a specific date range that added friction yielded an immediate list of hypotheses (e.g., checkout experiments, Europe checkout blocker). |
| **Forensic Implementation Review** | Codebase Query (Cursor, ChatGPT Deep Research connected to GitHub) | A detailed prompt directed the AI to act as a senior staff engineer and conduct a forensic investigation of code changes. |
| **Outcome** | Cursor/GitHub | Produced a comprehensive time-sequenced table listing every Pull Request (PR) affecting the feature, including links, summaries, affected users, and the impact explained in layman’s terms. This quickly identified a "smoking gun" experiment launched exactly when the drop occurred. |

*Querying the codebase allows non-technical users to trace implementation details, using code as a definitive source of truth. This speeds up problem crunching from weeks to hours.*

### 2. End-to-End Funnel Analysis for Feature Performance

This workflow details analyzing a feature change (like a payment signup flow redesign) that was not run as an A/B test.

1.  **Context from Code:** Cursor researches the codebase to determine exactly what was built, including the steps in the funnel and the front-end events emitted for analysis. This provides higher confidence than relying on documentation alone.
2.  **SQL Generation and Execution:** The analyst uses Cursor connected to the Snowflake MCP to generate and run SQL queries. The analyst instructs the agent to create the SQL file, use the MCP, and QA the output. Analysts manually QA the results, for example, by checking for expected drop-offs across steps.
3.  **Synthesis and Reporting:** The Mode MCP is used to analyze the resulting dashboard visualization, extracting detailed takeaways, insights, and actionable next steps. The Notion MCP is then used to draft the summary report following internal writing guidance, accelerating the production of a high-quality document.

*While AI provides a strong starting draft, human analysis and editing are still required for three to four revisions before creating an executive-ready document. The ability of the AI to comment on the SQL code it writes is useful for human review and understanding the underlying logic.*

### 3. Automating Experimentation Write-Ups

A custom agent built using a Cursor rules file automates the routine process of documenting A/B test results.

| Step | Agent Instruction/Tool Used | Output |
| :--- | :--- | :--- |
| **Data and Context Gathering** | Instructed to use the EPO MCP to pull results, and the Notion MCP to gather documentation (PRDs, specs). | The agent found the experiment results and relevant rules/documentation. |
| **Report Generation** | Instructed to write results in a specific, consistent format, including metrics, confidence intervals, and color-coding. | Generated a detailed report for the "vertical product tile images" experiment, showing a 3.5% lift. |
| **Decision and Communication** | Instructed to write a clear takeaway (roll out/roll back decision and rationale) and create a Notion document. | The agent correctly recommended rollout and provided a supporting rationale. It generated a Notion document and a summarized Slack message for quick approval. |

*This automation accelerates the documentation process, preventing the analytics team from becoming a bottleneck and allowing PMs and engineers to handle more analysis.*

### 4. Designing and Analyzing Unstructured Survey Data

AI transforms the time-consuming process of creating and analyzing customer surveys.

1.  **Survey Design:** Using a tool like ChatGPT Projects, background information (business context, strategy) and a list of specific hypotheses are uploaded. The model is prompted to design a survey, generate the Qualtrics coding file needed for implementation, and create an analysis plan.
2.  **Survey Analysis:** The raw, dense output file from Qualtrics is fed into the AI, along with a coding helper file. The AI is tasked with analyzing the data against the predefined hypotheses.
3.  **Outcome:** The AI produces a summary and a table judging each hypothesis as "proved," "neutral," or "disproved," accompanied by a confidence score and supporting insights.

*This workflow dramatically shortens the time required to move from hypotheses to initial findings, providing analysts with a better intuition for where to focus deeper analysis.*

## III. Impact and Strategic Benefits

The overall shift to AI-enhanced analysis creates significant organizational benefits:

*   **Focus on Strategy:** Analysts spend less time on tactical tasks (like writing repetitive SQL or editing documentation) and more time on high-level strategic tasks, generating creative ideas, and focusing on business impact.
*   **Democratization of Data:** Lowering the barrier to entry for data analysis allows non-analysts, including Product Managers (PMs), designers, and sales teams, to write SQL and conduct analysis, empowering them with necessary context.
*   **Acceleration and Efficiency:** AI accelerates the workflow, saving time for both the analysts and the leaders who consume their work, ensuring that insights reach the business rapidly.

## IV. Write Culture

The sources indicate that Faire (FAIR) has a very specific and formalized **write culture**, heavily focused on documentation and synthesized communication, especially for high-level analysis.

Key details regarding the writing culture at Faire:

### Formal Structure and Pre-Read Culture

*   Faire maintains a **"vertical doc culture"** and a **"pre-read culture"**.
*   The organization emphasizes **writing a lot of documents** rather than creating many slides.
*   The Chief Strategy Officer and other leaders on his team prioritize **synthesized writing**.
*   The Strategy and Analytics team developed specific **guidance on how to write at Faire**.
*   This guidance includes internal documents, such as the **"use answer for structure key principles doc"** and standard templates that define what documents should look like.
*   Analysis only matters if it can be communicated clearly to convince people of the intended message. The ability to draft a synthesized document is crucial for leveling up the quality of work.

### Role of AI in Writing and Documentation

AI tools have been integrated into workflows specifically to accelerate the creation and editing of these required documents:

*   **Accelerated Drafting:** The process of producing a summary report can be accelerated using AI tools like Cursor.
*   **Contextual Reporting:** The Notion Model Context Protocol (MCP) is used to direct Cursor to create a document that captures findings in a structured way.
*   **Rule Enforcement:** Analysts instruct AI agents (via prompts or cursor rules) to follow the specific internal writing rules and formats defined in their guidance documents when drafting reports. This ensures consistency, such as including specific metrics, confidence intervals, and color-coding in experiment write-ups.
*   **Automation of Routine Tasks:** Custom agents are built to automate routine documentation, such as the write-up of A/B test results, which helps prevent the analytics team from becoming a bottleneck and allows engineers and Product Managers to handle more analysis.
*   **Communication Delivery:** The AI can generate the Notion document and also spit out a more summarized version (e.g., a Slack message) for quick communication and approval.
*   **Source of Truth:** Analysts can query the product codebase (using tools like Cursor connected to GitHub) as a source of truth for marketing materials (like newsletters) or analysis, rather than relying solely on specifications or documentation written by Product Managers.

### Human Oversight and Quality

While AI accelerates the process dramatically, human judgment remains essential for final communication quality:

*   AI cannot yet "zero shot" (automatically generate in a single pass) an **executive-ready document**.
*   The AI-generated draft usually requires the human analyst to conduct **three to four revisions** of editing and adding analysis before it is complete.
*   LLMs are seen as valuable for checking the narrative structure, ensuring the story makes sense, and covering potential blind spots the analyst may have after deep analysis.

---
*The Strategy and Analytics team at Faire is currently hiring roles that partner closely with PMs and go-to-market teams, focusing on strategic data-driven decisions.*

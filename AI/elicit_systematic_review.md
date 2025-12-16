https://www.youtube.com/watch?v=mJXZuisO7vU

# Briefing Document: Elicit Automated Systematic Review Workflow

## I. Overview and Purpose

Elicit has developed a new workflow designed to automate the **entire systematic review process** from beginning to end. This comprehensive automation includes reporting search, screening, data extraction, and generating a preliminary report. The primary goal is to save researchers a significant amount of time, allowing them to focus more critically on the findings and results.

The platform aims to provide researchers with a much better understanding of the state of science on a given topic and help individuals making evidence-backed decisions. This workflow is built on an **automation-first** approach while maintaining **transparency and control** for the user.

## II. Target Audience

This systematic review workflow is specifically targeted toward **pro and power users** who are already familiar with the systematic review process and its steps. It is recommended that users understand how a systematic review is traditionally conducted, as the complexity might be overwhelming for novices.

## III. Core Workflow Steps

The systematic review process in Elicit follows these steps:

### 1. Refine Research Question

The process begins by asking a research question, such as "microplastics and pregnancy". Elicit provides feedback and suggestions to refine the question, which is crucial as it drives the subsequent steps. Suggestions often help specify the research focus, make the population more specific, or clarify how the outcome is measured.

### 2. Gather Paper Sources

Elicit allows users to collect papers through three methods:

*   **Elicit Search:** This uses semantic search across over 126 million papers from the Semantic Scholar database. Based on the research question, Elicit can automatically bring in **up to 500 relevant papers**. This is generally recommended as a supplement to traditional search methods (like Boolean searches on PubMed) to ensure comprehensiveness.
*   **Library:** Papers can be imported from the user's existing Elicit Library, potentially using tags.
*   **Upload PDFs:** Users can drag and drop or select PDFs to upload.

### 3. Define and Evaluate Screening Criteria

The system automatically generates custom screening criteria tailored to the research question.

*   **Defining Criteria:** Users can review suggested criteria (e.g., exposure assessment, study design, population) and choose to agree with them, change them, or turn them off. Users can also add their own custom criteria.
*   **Iteration and Transparency:** Initial iteration and refinement of criteria happen quickly using a smaller, randomly selected sample of 100 papers. For every paper evaluated against the criteria, Elicit provides an answer (Yes, No, Maybe) and a detailed explanation for that individual decision.
*   **Running on Full Set:** Once the criteria are finalized, the user runs the screening on the full set of papers (e.g., 500). Papers are ranked by their **likelihood of being included** based on how well they fit the screening criteria. Users can manually override any AI-generated judgment.

### 4. Data Extraction

Extraction also begins with a subset of screened-in papers to facilitate rapid iteration on field definitions.

*   **Extraction Fields:** Elicit automatically generates detailed extraction fields, often related to Pico elements, which are customized for the research question. These fields include detailed instructions and examples on how to extract the required data. Fields can be defined for free-form answers, selection from predefined options, or yes/no/maybe questions.
*   **Validation and Transparency:** To ensure accuracy, every AI-generated answer in the extraction step is accompanied by an asterisk, which, when clicked, reveals **direct quotes from the paper** (the ground truth). Explanations are also provided to help users understand the derivation of the answer.
*   **Scale:** Elicit can currently support large extraction tables, accommodating approximately 3,000 cells (e.g., 300 papers and 10 columns).

### 5. Generate Research Report

The final step is the automatic generation of a report, serving as a first draft or synthesis of the curated data.

*   **Report Content:** The report includes a detailed abstract, a methodology section (often Prisma-inspired), summaries of papers, and a detailed discussion intended to highlight themes across the literature.
*   **Interactivity:** Users can use a chat feature to ask follow-up questions about specific papers or analyze the underlying data in different ways. Reports can be downloaded as a PDF.

## IV. Key Benefits and Design Principles

| Feature | Description | Citation |
| :--- | :--- | :--- |
| **Transparency & Control** | Every AI-generated decision (screening judgment, extracted data point) is directly linked to supporting quotes or explanations from the underlying text, ensuring users can evaluate the work. Users can manually override any AI decision. | |
| **Iteration and Flexibility** | The system enables easy iteration; users can go back to previous steps (like refining criteria or definitions) and make changes without restarting the entire project. This is crucial because criteria often need adjustment based on the actual literature found. | |
| **Living Reviews** | By digitizing the workflow, researchers can easily update a review. If new papers are uploaded, they will automatically flow through the established screening criteria and extraction fields, taking only seconds, enabling the creation of "Living reviews". | |
| **Collaboration** | Users on specific plans can collaborate in real-time on the review. The work continues running in the background even if the browser is closed. | |
| **Time Savings** | Automation of data extraction alone can save teams a significant amount of time, sometimes up to six weeks, allowing them to reallocate effort toward critical thinking about the data. | |

***

*Analogy to solidify understanding:* Automating a systematic review with Elicit is like using a **self-driving car designed for professional mechanics**. The car handles the complicated travel route automatically (screening, extraction, report generation), saving immense time, but every single decision the car makes is logged and explained, allowing the expert mechanic (researcher) to easily take manual control, adjust the settings (criteria), and verify the precise data used for every action taken, ensuring high accuracy and reliability.

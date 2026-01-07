# Whitepaper: Automating Systematic Reviews with Elicit

## Executive Summary
Elicit has developed an end-to-end automated workflow for **systematic reviews**, designed to assist researchers in navigating the stages of search, screening, data extraction, and report writing. This "automation-first" approach is built on a foundation of **transparency and user control**, ensuring that every AI-generated decision is linked directly to source text and remains editable by the researcher. The primary objective is to significantly reduce the time spent on manual labor—potentially saving up to six weeks of work—allowing researchers to focus on critical thinking and the implications of their findings.

---

## Phase 1: Research Question Refinement
The process begins with the formulation of a research question. Because this question drives the subsequent automation steps, Elicit provides **AI-generated feedback** to ensure the query is specific and well-defined.
*   **Suggestions:** If a question is too vague (e.g., "microplastics and pregnancy"), the system suggests narrowing the focus to specific populations, exposure types, or outcome measurements.
*   **Automation Settings:** Users can choose to "populate steps with suggestions based on research question," allowing the AI to draft the initial criteria for screening and extraction.

## Phase 2: Paper Collection (The Gather Step)
Elicit allows users to aggregate a broad universe of papers from multiple sources into a centralized library.
*   **Elicit Search:** Users can automatically import up to **500 papers** using semantic search, which identifies relevant titles and abstracts from a database of 126 million papers.
*   **External Integration:** Elicit is intended to supplement traditional Boolean search methods (like PubMed). Researchers can conduct their standard searches and **upload the resulting PDFs** to ensure comprehensiveness.
*   **Library and Tags:** Papers can also be imported from existing Elicit libraries or filtered via user-defined tags.

## Phase 3: Screening and Criteria Iteration
The screening step is designed to narrow down the collected papers into a finalized set for review.
*   **Custom Criteria:** Elicit generates **suggested screening columns** (e.g., "Is the study conducted in humans?") based on the specific research question.
*   **Iterative Sampling:** To ensure speed and cost-efficiency, the system first runs these criteria on a **representative sample of 100 papers**. This allows researchers to refine their criteria before applying them to the full set.
*   **Transparency:** For every "Yes/No/Maybe" judgment, Elicit provides an explanation and links the decision to specific sections of the paper’s abstract.
*   **Manual Overrides:** Researchers can rank papers by their likelihood of inclusion and manually override any AI decision to maintain full control over the final selection.

## Phase 4: Data Extraction
Once papers are screened in, the system automates the extraction of specific data points.
*   **PICO and Custom Fields:** Elicit suggests fields for extraction, such as participant characteristics, study design, and exposure assessments, providing detailed instructions for the AI to follow.
*   **Ground Truth Verification:** Every extracted value is marked with an asterisk; clicking it reveals **direct quotes from the text or tables**, ensuring the information is one click away from the source.
*   **Capacity:** The system currently supports tables of approximately 3,000 cells (e.g., 300 papers with 10 columns).

## Phase 5: Synthesis and Reporting
The final stage involves generating a research report that serves as a first draft for the final review.
*   **Report Components:** The report includes a Prisma-inspired diagram, a summary of study methods, a detailed discussion of themes across the literature, and a complete references list.
*   **Interactive Chat:** Users can **chat with the report** to ask follow-up questions about specific papers or analyze the data from different perspectives.
*   **Export and Sharing:** Results can be exported as CSV or PDF files, and teams can collaborate on the review in real-time.

---

## Conclusion: Living Reviews
Unlike manual reviews that often become outdated by the time of publication, Elicit’s digital workflow supports **"Living Reviews"**. Once the screening and extraction criteria are defined, new papers can be added to the project, and they will automatically flow through the established process in seconds.

**The Elicit workflow acts like a high-powered filter in a digital laboratory; you set the parameters and pour in the raw data, and the system instantly sifts out the impurities, leaving you with a refined, concentrated extract ready for final analysis.**

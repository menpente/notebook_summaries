# Briefing Document: Agentic Analytics in Production

## Executive Summary
This document outlines the architecture and implementation strategy for **agentic analytics**, specifically focusing on the development of a "Talk-to-Your-Data" Slackbot. The primary goal is to address **decision latency** by enabling non-technical stakeholders to access data insights rapidly without waiting for the traditional data team ticket cycle. The core of a successful system lies not just in AI intelligence, but in the **semantic layer** that provides necessary business context.

---

## 1. The Core Problem: Decision Latency
In typical analytics workflows, stakeholders formalize ideas into questions for the data team. However, this often fails because:
*   **Time Delays:** Tickets sit in backlogs for weeks.
*   **Clarification Loops:** Analysts often need to go back to stakeholders for extra context.
*   **Data Issues:** Data is frequently messier than expected.

**Agentic Analytics** serves as an enabler for early insights, allowing stakeholders to verify ideas before they even reach the data team.

---

## 2. Architecture: The Dual-Subsystem Design
To simplify the process of turning natural language into insights, the system is broken down into two distinct subsystems.

### Subsystem 1: The Routing System (Natural Language to Data)
This system identifies the user's intent and maps it to the correct data table.
*   **Mechanism:** It utilizes a **metrics catalog** derived from the semantic layer.
*   **Components:** 
    *   **LLM Mapper:** Maps the question to candidate tables.
    *   **LLM Assessor:** Acts as a judge to score tables based on how well they suit the question.
*   **Current Limitation:** The MVP typically supports **single-table routing** rather than complex multi-table joins.

### Subsystem 2: The Analyst Agent (Data to Insights)
Once the data is identified, this system analyzes it to provide answers.
*   **Technology Choice:** The sources recommend **PandasAI** for MVPs over complex "Text-to-SQL" systems.
*   **Benefits of PandasAI:** It is open-source, uses flexible Python code, and includes built-in support for summaries and charts.
*   **Context Loading:** It requires both the raw data and the semantic context (YAML files) to function effectively.

---

## 3. The Semantic Layer: The "Secret Sauce"
The most common reason agentic systems fail is a **misunderstanding of business context**. The semantic layer lives on top of data sources to provide:
*   **Definitions:** Clear meanings for business metrics.
*   **Relationships:** How tables relate from a business perspective.
*   **Format:** Typically implemented via **YAML files** containing dimensions, grain filters, and business-friendly descriptions.

---

## 4. Moving from Prototype to Production
Intelligence alone does not make a system production-ready; it must be predictable and maintainable.

### Input Guardrails (Question Validation)
Preventing "bad data" from entering the system is more critical than filtering output. 
*   **Rubric-Based Validation:** An **LLM as a judge** checks questions for **Metric Clarity**, **Slice Clarity**, and **Time Clarity**.
*   **User Feedback:** If a question is too ambiguous, the system asks for clarification before wasting computational credits.

### Operational Excellence
*   **AI Workflows vs. Agents:** Focus on **predictable workflows** with predefined paths rather than fully autonomous agents that "run wild".
*   **Observability:** Implement logs and state tracking from day one to monitor costs (e.g., OpenAI API spend) and system failures.
*   **Deployment:** Use resource-aware deployment strategies (like Kubernetes) to handle concurrent user requests.

---

## 5. User Adoption and Strategy
*   **Ideal User Profile:** Start with a specific group, such as **Product Managers (PMs)**, who are data-savvy and benefit most from quick insights.
*   **Controlled Rollout:** Use feedback sessions and video walkthroughs to build "hype" and ensure the system meets real expectations before a company-wide launch.
*   **Feedback Loops:** Include simple UI elements like **thumbs up/down** to collect qualitative data on response accuracy.

---

## 6. Future Trends
Agentic analytics is expected to be a defining trend through 2026. Organizations are increasingly moving toward the **commoditization of the semantic layer**, with major BI vendors (Looker, PowerBI, Cube) investing heavily in AI-compatible semantic tooling.

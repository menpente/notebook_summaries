https://arxiv.org/pdf/2510.23587

# Briefing Document: A Hierarchical Taxonomy for Data Agents (L0-L5)

## Overview and Context

This document summarizes the systematic hierarchical taxonomy proposed for classifying **Data Agents**.

A Data Agent is defined as a comprehensive, **Large Language Model (LLM)-powered architecture that orchestrates the Data + AI ecosystem to autonomously perform a wide range of data-related tasks**. These tasks span the data lifecycle, including Data Management (Configuration Tuning, Query Optimization, System Diagnosis), Data Preparation (Cleaning, Integration, Discovery), and Data Analysis (Structured/Unstructured Analysis, Report Generation).

### The Need for a Taxonomy

The term "data agent" currently suffers from **terminological ambiguity and inconsistent adoption**, conflating simple query responders with sophisticated autonomous architectures. This ambiguity leads to:

*   **User-Side Risk:** Expectation mismatches regarding the agent's scope and limitations, which can lead to undue reliance on erroneous outputs.
*   **Governance Risk:** Indistinct lines of responsibility when failures occur (e.g., data leakage or erroneous reports), challenging accountability.
*   **Industry-Side Risk:** Erosion of market confidence due to overstated claims and blurred capabilities, hindering objective system comparison.

Inspired by the SAE J3016 standard for driving automation, this taxonomy introduces **six levels (L0-L5)** that delineate and trace progressive shifts in autonomy, clarifying capability boundaries and responsibility allocation.

***

## Hierarchical Autonomy Levels of Data Agents

The hierarchy is structured around the progressive transfer of dominance and responsibility from the human to the data agent.

| Level | Autonomy Designation | Human Role (Control & Responsibility) | Data Agent Role (Functionality) | Evolutionary Leap |
| :---: | :---: | :--- | :--- | :--- |
| **L0** | **No Autonomy** | **Human in charge**; All tasks are entirely human-driven. Humans are **solo practitioners**. | Uninvolved. | N/A |
| **L1** | **Assistance** | Humans retain task dominance and responsibility for integration, verification, and interacting with the environment. Humans shift from solo practitioners to **users of query-responsive assistants**. | Provides **preliminary, stateless assistance** for isolated tasks. Functions as a nascent intelligent assistant within a prompt-response framework. | Introducing Assistance (L0 to L1) |
| **L2** | **Partial Autonomy** | Humans are responsible for **managing the overall workflow** and retain dominance over tasks (e.g., orchestrating pipelines). | Gains the ability to **perceive and interact with the environment** (e.g., data lakes, tools, APIs). Acts as a **procedural executor** within human-orchestrated pipelines. | Gaining Perception (L1 to L2) |
| **L3** | **Conditional Autonomy** | Humans act as **supervisors** overseeing the agent’s operation, but the agent assumes the dominant role in tasks. | **Autonomously orchestrates and optimizes tailored data pipelines** for diverse and comprehensive data-related tasks. Evolves from procedural executor to a **versatile dominator**. | Transfer of Task Dominance (L2 to L3) |
| **L4** | **High Autonomy** | Humans fully delegate responsibility, becoming **onlookers** and recipients of insights. | Achieves high autonomy and reliability, operating **independently of human supervision**. Can **proactively identify issues** and autonomously orchestrate pipelines to tackle self-discovered problems. | Removing Supervision (L3 to L4) |
| **L5** | **Full Autonomy** | **Complete disengagement**; any form of human involvement is unnecessary. | Functions as a **generative data scientist** capable of inventing novel solutions and pioneering new paradigms. | Innovating and Pioneering (L4 to L5) |

***

## Current Evolutionary Focus (L2 to L3 Transition)

The field is currently focused on the **L2-to-L3 transition**, where agents must evolve from procedural execution to autonomous orchestration.

### Proto-L3 Systems

No existing system has fully realized the versatile, self-directed orchestration capabilities of a complete L3 data agent; however, **emerging efforts are termed "Proto-L3"**. These systems exhibit nascent potential toward conditional autonomy by attempting autonomous pipeline orchestration.

Examples of Proto-L3 efforts include:

*   **Orchestration:** Systems like Data Interpreter recast pipeline orchestration as a Hierarchical Graph Modeling problem, allowing dynamic plan modification based on executor feedback.
*   **Broadened Scope:** Some systems, such as iDataLake and AOP, extend task coverage across heterogeneous data lakes, managing cleaning, integration, discovery, and analytics.
*   **Tool Evolution:** JoyAgent introduces a "Tool Evolution" capability that dynamically creates new tools by reassembling existing atomic tools, partially overcoming the limitation of fixed toolsets.

### Challenges Toward True L3 Autonomy

Several challenges hinder the realization of true L3 autonomy:

1.  **Limited Autonomy in Pipeline Orchestration:** Proto-L3 agents still rely heavily on **predefined operations or tools**. Achieving true L3 requires future research to integrate **continuous skill discovery** with pipeline orchestration, enabling agents to generate, evaluate, and deploy both predefined and emergent skills.
2.  **Incomplete Coverage of the Data Lifecycle:** Current Proto-L3 systems often focus narrowly on data analysis, lacking robust capabilities in crucial data management tasks like database configuration tuning or system diagnosis.
3.  **Deficiencies in Advanced Reasoning:** Agents currently lack **higher-order reasoning** to adapt their overarching strategy, often getting trapped in loops that treat symptoms rather than diagnosing and resolving root causes.

***

## Future Vision (L4 and L5)

### L4: High Autonomy

L4 data agents will function as trustworthy, proactive, and self-governing agents. This requires:

*   **Autonomous Problem Discovery:** L4 agents must continuously monitor and explore data lakes to **proactively identify valuable and emerging tasks** without explicit human instructions.
*   **Long-Horizon and Holistic Views:** Agents must possess long-term planning capabilities and optimize across processes, balancing trade-offs (e.g., computational costs of cleaning vs. long-term analytical benefits).

### L5: Full Autonomy

L5 is the ultimate vision, where the agent functions as a fully autonomous and generative data scientist. The agent not only applies existing methods but also **actively creates new knowledge** by recognizing when conventional approaches fail and inventing novel theories, algorithms, or paradigms.

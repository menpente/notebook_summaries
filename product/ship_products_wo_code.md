# Briefing Doc: Shipping Products with AI (The Zevi Arnovitz Workflow)

This briefing document outlines the strategies and workflows used by **Zevi Arnovitz**, a Product Manager at Meta, to build and ship significant software products without a technical background,. It highlights the shift toward "vibe coding" and how non-technical leaders can leverage AI as a "superpower" to become builders,.

---

## Executive Summary
The sources describe a paradigm shift where **titles and responsibilities are collapsing** due to AI. Zevi Arnovitz, who has no formal technical training, demonstrates that a PM can manage the entire product lifecycle—from ideation to deployment—by acting as the "owner of the problem" while treating AI agents as a specialized engineering team,.

## Core Tools and Evolution
Arnovitz suggests a graduated "exposure therapy" approach for non-technical individuals who may find code terrifying:
*   **Phase 1: Chat Interfaces.** Starting with **ChatGPT or Claude Projects** to compartmentalize knowledge and instructions,.
*   **Phase 2: Specialized Build Tools.** Graduating to platforms like **Bolt or Lovable** that are "eager to write code" and provide rapid UI generation,.
*   **Phase 3: Advanced IDEs.** Finally moving to **Cursor with Claude Code**, which offers deep access to the codebase and allows for complex, multi-model workflows,.

---

## The "Vibe Coding" Workflow
The sources detail a specific, repeatable workflow using custom **slash (/) commands** within Cursor to maintain high standards and technical rigor,.

### 1. Issue Capture (`/create issue`)
*   **Purpose:** Quickly capture bugs or feature ideas during development without breaking flow,.
*   **Action:** Uses AI to generate a structured ticket directly in **Linear**, including TLDRs and expected outcomes,,.

### 2. Exploration Phase (`/exploration`)
*   **Purpose:** Ideation and technical discovery.
*   **Action:** The AI (acting as a CTO) analyzes the existing codebase to understand the current state and asks the PM clarifying questions about data models, UI/UX, and validation,,.

### 3. Planning (`/create plan`)
*   **Purpose:** Avoiding "gnarly bugs" caused by coding agents jumping straight into implementation.
*   **Action:** Generates a **markdown plan** with tasks, status trackers, and critical decisions,. This plan acts as a source of truth that can be executed by different AI models.

### 4. Execution (`/execute plan`)
*   **Purpose:** Building the feature.
*   **Action:** Uses high-speed models like **Cursor’s Composer** to implement the plan across multiple files,.

### 5. Multi-Model Peer Review (`/review` & `/peer review`)
*   **Purpose:** Mitigating the PM's inability to manually review code for errors,.
*   **Action:** Arnovitz employs different models to "fight it out":
    *   **Claude:** Acts as a communicative, opinionated CTO.
    *   **Codex (GPT-4o):** Acts as the "coder in a dark room" who solves difficult bugs but is less communicative,.
    *   **Gemini:** Acts as a "crazy scientist" who is exceptional at design but has a volatile thought process,.

### 6. Documentation and Learning (`/update docs`)
*   **Purpose:** Making the codebase "AI-native".
*   **Action:** Updates markdown files within the code to explain high-level structures to future AI agents, ensuring they don’t repeat past mistakes,.

---

## Strategic Insights for Non-Technical Leaders

*   **Treating AI as People:** Arnovitz mitigates "sycophantic" AI behavior (where the model agrees with bad ideas) by explicitly instructing the AI to act as a **CTO who challenges the user** and takes complete technical ownership,,.
*   **The Learning Opportunity:** Use the command `/learning opportunity` to have AI explain complex architectural decisions using the 80/20 rule, effectively turning product building into a "tuition" for technical growth,,.
*   **Career Growth:** Arnovitz argues it is the **best time to be a junior** because individuals can now build and iterate on their own startups or side projects (like StudyMate) to gain "reps" and product sense that would otherwise take years to acquire at a large company,,.
*   **Human-Centric Skills:** As technical barriers fall, the most valuable traits become **curiosity, communication, and a "growth mindset"**,. Arnovitz emphasizes that AI doesn't replace thinking; rather, the person who is better at using AI will replace the one who isn't,.

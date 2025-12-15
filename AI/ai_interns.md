https://www.youtube.com/watch?v=SXCtQnJE8_I

# Briefing: AI Automation for Executive Assistants at Zapier

This document outlines how Zapier's Executive Assistant (EA) leverages AI tools, particularly Zapier Agents and custom GPTs, to automate key administrative and strategic tasks, transforming the EA role into a high-leverage function that scales organizational efficiency and reinforces company culture.

## I. AI Mindset and Role Transformation

The adoption of AI tools by EAs is seen as a "when, not an if" necessity. The primary goal is to **automate the repetitive, boring, and manual parts of the role** to allow the EA to focus on more interesting, creative, human-centric, and relationship-driven work. AI agents are conceptualized as "interns" that, once taught the necessary system, can operate and perform tasks on their own, allowing the EA to systematize leverage across the organization.

A key recommendation for adopting AI is: if a task is repeated every week, spend time that week automating it into an agent.

## II. Core Workflow: Automated Weekly Meeting Prep Agent

The EA built a **Weekly Meeting Prep Agent** using Zapier Agents, which allows for complex tasks involving reasoning and freedom to operate. This agent replaces a manual preparation process that previously took about an hour every Friday.

| Agent Function | Details and Steps | Source Citation |
| :--- | :--- | :--- |
| **Trigger & Scope** | The agent is scheduled to trigger weekly (e.g., Friday at 8 a.m.) and pulls the calendar for the upcoming week. It focuses on meetings requiring prep, typically external meetings, and excludes recurring internal meetings like standups or one-on-ones. | |
| **Research Buddy** | For external participants (those without a Zapier email), the agent conducts a web search to identify their current role, industry experience, and any noteworthy information. | |
| **Internal Context Gathering** | It checks the company's CRM (HubSpot) using integrations to find the participant's relationship with Zapier, including deal status or recent sales team notes. It also searches internal communication history (Gmail and Slack) for prior relationships or callouts related to their company. | |
| **Output 1: To-do List Task** | Creates a task in the EA's to-do list app (To-doist) containing all the gathered intelligence and scheduling the prep time two hours before the meeting. | |
| **Output 2: Weekly Slack Digest** | Delivers a structured digest to Slack, including meeting intelligence, necessary error handling (e.g., if a participant couldn't be found), and **key prep recommendations** that leverage the agent's creativity. | |

This agent serves as a "second brain" by consolidating context from the CRM, email, and Slack into one place for a quick memory refresh.

## III. Reinforcing Culture: Meeting Feedback and Coaching

A workflow was developed to provide meeting coaching, serving as an accountability mechanism and reinforcing cultural values (like "growth feedback") and operating principles.

*   **Process:** The system utilizes meeting transcripts (from tools like Fathom or Fellow) and meeting metadata.
*   **Parameters:** Feedback is only generated for Zapier employees when there is sufficient context and if the meeting meets specific criteria (e.g., not just 10 minutes long).
*   **Context:** The agent is given extensive context on company values, meeting norms, decision-making philosophies, and Zapier’s desired impact behaviors. It also uses frameworks like the "five dysfunctions of a team".
*   **Feedback Style:** Feedback is delivered in a style that is both **demanding and supportive**, offering direct constructive feedback. It clarifies that the feedback is **AI-generated** and provides one to two specific growth opportunities and one to two things the participant can do next time.
*   **Impact:** This automation helps normalize feedback within the organization, making it expected and less stressful, and ensuring leaders consistently display company values.

## IV. Scaling Executive Alignment: The Exec GPT

To address the bottleneck of EAs providing individual thought partnership on strategic documents, an **Exec GPT** (built on OpenAI’s platform) was created to stress-test "T-up" documents before they reach executives.

*   **Goal:** The GPT helps people sharpen their T-ups, ensuring the right data is included, opinions are stress-tested, and that meetings are as productive as possible—sometimes allowing meetings to be skipped entirely if the document is clear enough.
*   **Knowledge Base:** The GPT is built on context provided by the EA, including team norms, the revenue roadmap, the strategy memo, good T-up examples, and specific documents related to the CEO's feedback and tuning.
*   **Output:** The GPT provides feedback on strengthening the document, surfacing trade-offs, and adding recommendations. For example, it might suggest a "Wade style one-page rewrite" for documents that are too loose. It also provides a "bold coaching question" for discussion in the meeting ("bullpen").

## V. Strategy Companion for Internal Alignment

To ensure organization-wide strategic thinking and alignment, a **Strategy Companion** was launched using Notebook LM (enabled through Google).

*   **Purpose:** This tool serves as an interactive strategy companion, helping employees understand how top-level strategy impacts their daily work and find answers easily.
*   **Knowledge Base:** The companion aggregates dozens of sources, including the top-level strategy document, all-hands meeting transcripts, and every organization's strategic action plan.
*   **Access:** Users can interact with the knowledge base in a chat capacity, asking specific questions like, "As an executive assistant, how can I contribute to Zapier's 2026 strategy?".
*   **Multimodal Output:** The tool can generate interactive content, such as an AI-generated podcast based on the source material, ensuring the strategy is not a static document.

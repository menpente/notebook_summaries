# Briefing Document: The Jira Product Discovery Process

This briefing outlines a four-stage product discovery process ("Wonder," "Explore," "Make," and "Impact") used by the Jira Product Discovery team at Atlassian. This process emphasizes rapid customer feedback, iterative solution development, and a cautious scaling strategy to ensure product success.

---

## 1. Overview of the Discovery Process

Product discovery is considered the number one high-leverage task for a Product Manager (PM). The Jira Product Discovery team's process is designed to bring clarity to complex problem areas, moving from fuzzy ideas to validated solutions.

The four main stages, used both at the macro level (for the whole product) and the micro level (for specific features), are:

1.  **Wonder** (Problem Exploration)
2.  **Explore** (Solution Exploration)
3.  **Make** (Commitment to Building)
4.  **Impact** (Measurement and Iteration)

The entire process is viewed as a continuous cycle, rather than a strict waterfall, where learning in one stage influences movement to the next.

---

## 2. Deep Dive into the Stages

### A. Wonder Stage: Unpacking the Problem

**Focus:** Problem exploration and understanding the pain points.

**Methodology:**
*   The team conducts about **a dozen user interviews** to unpack a problem area, continuing until the same themes repeatedly emerge.
*   The research style is highly focused on hearing **raw emotions** and the problem in the **customer’s own words**, akin to ethnographic research.
*   PMs are advised to stop interviews once **convergence on insights** is reached and the "sand is starting to settle," indicating clarity.

**Deliverable:**
*   The typical outcome is a document that identifies who the team is trying to help and the problems they face, often focusing on specific personas (e.g., product ops, PMs, VPs).
*   The most crucial part is a compilation of **less than 10 minutes of customer video clips**. This visual evidence is highly effective at triggering urgency and action within the team, more so than beautifully written abstract summaries.
*   Tools like **Dovetail** are used to manage user interviews, create transcripts, and generate video snippets, while **Loom** can be used for compiling these snippets into a story.

### B. Explore Stage: Validating the Solution

**Focus:** Solution exploration and achieving validation that a potential solution would actually solve the user's problem.

**Methodology:**
*   The goal is **not** to create finished designs, but to find quick ways to test concepts with users.
*   PMs are asked to go back to the customers used in the Wonder stage to show solutions and have them explain how the concept solves their pain.
*   Prototypes are often **low-fidelity** and simple, such as using a slide deck to present different product pillars or concepts.
*   The team uses tools like **Lovable** to upload Figma screenshots and turn them into interactive prototypes, maintaining a low-fi feel so users understand it's not a final product.
*   Prior to exiting Explore, the team might conduct a **technical spike** (a brief two-week attempt in the code) to prove technical feasibility and inform the complexity of the future build.

### C. Make Stage: Building and Scaling Safely

**Focus:** Committing to building the solution after achieving sufficient customer validation.

**Scaling Strategy (The Safety Funnel):**
*   The team employs a cautious, progressive rollout process (dubbed the **Safety Funnel**) to **minimize the number of people who have a bad experience**.
*   The progression involves working with a small group (e.g., 10 customers), then scaling to a larger group (100), and then progressively to an even larger base (1,000). This ensures the product is ready for the environment and maintains high user satisfaction (CSAT).
*   Winning back a customer who had an early, poor experience is much harder than waiting until the product is ready.

**Development & Iteration:**
*   During Make, design is often **reset**, and iteration starts again, now with engineers, designers, and PMs collaborating daily.
*   A **live feature document** is used by the whole team (not Jira) to define the scope of the Version 0 build, allowing the scope to expand and contract as understanding grows.
*   To enable fast iteration, PMs test changes directly from engineering branches (e.g., via a Chrome extension/Bitbucket integration) even if the code is just a micro change or throwaway branch. The team aims to get something into customer hands in about one to three months, even if the feature takes six or more months to be fully ready.

### D. Impact Stage: Measuring Outcomes

**Focus:** Measuring product performance after launch against desired goals.

**Methodology:**
*   An **impact page** is typically written a few months after launch to document the product's performance.
*   Decisions are then made on how to proceed: whether to retire the feature, leave it for a small customer base, put it on hold, or invest in a longer-term roadmap for future iterations.

---

## 3. Key Tactics for Customer Knowledge and Tooling

The foundation of this process relies on quickly learning about customers, which is seen as providing an **unfair advantage** over competitors.

### A. Feedback Intake and Mechanics
*   PMs are encouraged to set up the mechanics (recruiting, scheduling, recording) so that the process of obtaining feedback takes "no thinking whatsoever".
*   **Tooling Used:**
    *   **Dovetail:** Stores user interviews, creates transcripts, and allows querying transcripts for themes and snippet creation.
    *   **Pendo:** Used for running segments to identify customers to talk to and for conducting in-app questions (e.g., A/B testing or CSAT).
    *   **Jira Service Management:** Used as a queue to receive and triage raw feedback.
    *   **Calendly/Email:** Simplifies scheduling with customers using quick, human, two-liner emails.
*   Despite scaling to 18,000 customers, the team maintains close contact with users through community groups and Slack "speed dial" lists.

### B. High-Quality Interview Practices
PMs are strongly advised to seek **training from a real user researcher** to drastically improve interview quality.

| Poor Practice | Recommended Practice | Source |
| :--- | :--- | :--- |
| Leading conversations or pushing users in specific directions. | Use a simple script (introduction, role description) and then rebound on what they say; **do not ask leading questions**. | |
| Interrupting the user while they are talking. | **Never interrupt** a user who is talking. | |
| Giving the user response options. | Ask an open question (e.g., "What's the first thing you do in the morning?") and then **sit on your hands and wait** through the uncomfortable silence. | |

By hearing customer pain in their own words, the PM team ensures they are getting perspectives they did not have and continue learning.

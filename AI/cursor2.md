https://www.youtube.com/watch?v=2aldTxnbNt0

This briefing document outlines the key concepts, features, and comparative analysis of Cursor, drawing from the provided tutorial transcript excerpts.

***

# Cursor 2.0 Tutorial Briefing

This comprehensive course is designed to take users from zero to hero, enabling them to confidently use Cursor to vibe code landing pages, desktop apps, or anything imaginable. The tutorial covers foundational concepts, advanced features of Cursor 2.0, and a workflow for building, scaling, and deploying a full-stack application.

## I. Cursor: Definition and Core Identity

Cursor is defined as an **IDE** (Integrated Development Environment), often described as **VS Code's cousin**. It stands out among most vibe coding tools as probably the **only real true IDE**.

### Key Advantages of Using Cursor

1.  **Solid Foundation and High Ceiling:** Cursor helps users build a strong foundation for vibe coding and is a platform they can grow into, as the skill ceiling is very high. Real programmers, including professional engineers, use Cursor, exposing users to the ecosystem and extensions common to VS Code.
2.  **Local Application:** Unlike many web-based competitors (like Replet), Cursor is an application that lives directly on the user's laptop. This localization means the code exists on the user's computer, giving them more control, allowing interaction with the desktop view (e.g., drag and drop files), and supporting the creation of nearly anything that code can do:
    *   Mobile apps.
    *   Indie games.
    *   Embedded systems (e.g., programming a keyboard).
    *   Landing pages and websites.
3.  **Community and Support:** Cursor is described as the most established player in the vibe coding space, having been around for years. Its connection to VS Code means users benefit from a large community and available extensions.

## II. Key Features and Workflow Concepts

Cursor 2.0 introduced significant updates focused on AI and user experience.

### A. AI Agent and Interaction Modes

The core AI component is the **Agent**, which is elevated AI given specific tools that allow it to create and edit files, and execute necessary actions to write code.

Cursor offers three primary interaction modes (accessible via `Shift + Tab`):

| Mode | Functionality | Usage |
| :--- | :--- | :--- |
| **Ask Mode** | Purely answers questions; does not run code or edit files. | Great for learning and understanding concepts (e.g., "How do I play the game?"). |
| **Agent Mode** | Has full control over all tools (writing, editing, running servers). | Used for generating code and making functional changes. |
| **Plan Mode** | Generates an action plan without immediately writing code; often asks clarifying questions. | Useful for complex tasks or if the user is lazy about detailed prompt engineering. The generated plan is an editable markdown file that feeds context into the agent. |

### B. Agent Customization and Context

1.  **Rules:** Users can create rules (Project Rules for specific projects, or User Rules that follow them everywhere) to guide the agent's behavior and avoid unwanted patterns (e.g., banning specific colors or emojis).
2.  **Commands:** Users can create custom shortcuts (e.g., `/commit`) to automate complex or frequently used interactions with the agent, such as running Git commands.
3.  **Indexing and Docs:** The agent's power hinges on the context it is given. Users can provide documentation links (e.g., Instant DB documentation) for the AI to read, comb, and index, effectively teaching the AI how to use new technologies or APIs.
4.  **Contextual Reference (@ Feature):** Users can specifically point the agent to parts of the project for context:
    *   **@file:** Attaches the entire content of a specific file for reference.
    *   **@folder:** Appends a condensed summary of the files and subfolders, rather than the entire line-by-line code.
    *   **@browser:** Allows the agent to look at the currently running local website (by capturing a screenshot), useful for debugging layout or overflow issues.
5.  **Concurrent Agents (Cursor 2.0):** Users can run multiple agents (e.g., Composer 1, GPT-5, Sonnet 4.5) simultaneously to tackle a problem, providing several solutions to test. This feature requires a paid plan and a Git repository.
6.  **Composer 1:** Cursor's proprietary model, noted for being **insanely fast**—significantly faster than Sonnet 4.5 and GPT models.

### C. Development and Deployment

1.  **Local Development:** Code can be run locally on the user's computer (which acts as the server), speeding up the development process significantly.
2.  **Git:** Git is used for version control, allowing coders to set "checkpoints" or "saves" of their project. Git initialization is necessary to use multiple concurrent agents.
3.  **Full Stack Development:** Full stack means the application includes both the front end (what the user sees, often called `source` or `components`) and the backend (functionality the user doesn't see, such as data handling and authentication).
4.  **Deployment (Versell):** To deploy an application (make it public on the internet), users can utilize the Versell CLI (Command Line Interface). Versell is recommended for Next.js applications. The deployment process involves: pushing code to GitHub (the cloud version of Git), signing into the Versell CLI, and then deploying the project.

## III. Competitive Landscape Comparison

The following table compares Cursor with other major players in the vibe coding space based on criteria discussed in the tutorial:

| Feature | Cursor | Replet | Vzero | Lovable |
| :--- | :--- | :--- | :--- | :--- |
| **Backend Support** | Moderate/High Skill Cap. Pick your own stack (Instant DB, Superbase). | Offers both in-house and easy external database solutions. | Uses Superbase via partnership (requires manual linking). | Uses Lovable Cloud (Superbase wrapper). Highly locked-in. |
| **Speed** | Fastest. Composer 1 is insanely fast. | Slower but often provides high-quality, thought-out results. | Fast (Comparable to Lovable). | Fast (Comparable to Vzero). |
| **Model Selection** | Full freedom (Composer, Sonnet, GPT, Codeex, local LLMs). | Uses Anthropic/GPT models. | Uses Vzero Model (trained for Next.js). | Uses Anthropic/GPT models. |
| **Effort to Share** | High/Hard. Requires manual setup (Git, Versell CLI deployment). | Easy. Automatically hosts a public link. | Easiest. One-click deploy; automatically deploys to Versell. | Easy. Automatically hosts a public link. |
| **Experience/User** | **Prosumer/Professional.** Highest skill ceiling, provides maximum flexibility and growth potential. | Intermediate vibe coder. | Intermediate/Beginner vibe coder. | **Beginner/Kids.** Super approachable; low skill ceiling; often only creates websites. |
| **Price** | Flexible. Allows users to control token and hosting costs. | Highest risk of high usage bills due to powerful, long-running agents. | Comparable to Lovable; takes a premium on top of hosting costs. | Comparable to Vzero; complex credit system and premium on hosting costs. |

***

> **Analogy:** Using Cursor is like using **Photoshop** for creative development—it has a steep learning curve and requires expertise, but it offers unparalleled power, flexibility, and the ability to handle every complexity imaginable. Competitors like Lovable and Vzero are more akin to **Canva**—quick, easy to use for simple tasks (like websites/landing pages), but ultimately limiting creativity and flexibility for highly complex or specific projects.

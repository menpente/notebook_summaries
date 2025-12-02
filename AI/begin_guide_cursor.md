https://youtu.be/Gqpk7-FruqI

# Briefing: Coding with Cursor (AI Code Editor)

This document summarizes key features, best practices, and use cases of Cursor, an AI code editor and IDE, based on the provided transcript.

---

## 1. Overview and Core Functionality

**Cursor is an AI code editor** that integrates models from top labs (like OpenAI, Anthropic, and Google) and also trains its own custom models for tasks such as predicting actions or applying code. Cursor is designed to support a spectrum of users, ranging from beginners who are just starting with coding to experienced power users.

The editor interface typically utilizes three panels:

1.  **Left Panel:** Displays the directory and files of the application.
2.  **Middle Panel:** Where the user views a specific file or looks at changes they want to make.
3.  **Right Panel (Agent):** Features the AI agent, which represents an increase in autonomy and can write entire files for the user.

Basic AI functionality includes helpful **autocomplete suggestions** when typing code or importing necessary code.

## 2. The AI Agent and Autonomy

The Cursor agent is designed to manage tasks with high autonomy, akin to putting a destination into a GPS and letting it figure out the steps along the way.

The AI agents are given **"skills"** to read and search files in the codebase and run various commands.

### Example: Fixing Lint Errors
The agent can be instructed simply to "fix the lint errors". The agent will then:

1.  Determine the necessary terminal command (e.g., `bun run lint`).
2.  Run the command, identify the issues (such as a type error like `any`).
3.  Apply the required code changes.
4.  Rerun the command to **verify itself** that the issues were fixed.

The agent provides output detailing what it did, such as fixing type safety issues and formatting the code. Additionally, the agent can perform tasks, like adding a new route, in the background while the user continues working in the main view.

## 3. Best Practices for AI-Assisted Development

To make the codebase more resilient to errors and enable AI models to fix problems more effectively, traditional software engineering techniques should be applied:

| Concept | Explanation | Benefit for AI |
| :--- | :--- | :--- |
| **Typed Languages** (e.g., TypeScript) | Forces the use of specific data types (like string, boolean, etc.). It makes writing code more strict. | Helps prevent issues and provides feedback to AI agents when generated code is potentially wrong, allowing the agent to self-correct. |
| **Llinters** | Reviews code for common errors and formatting issues. | Provides opinions about how code is written and helps find and fix errors based on common developer mistakes. |
| **Formatters** | Automatically structures the code correctly, handling line breaks, tabs, and style. | Removes the need for the developer or AI to focus on formatting. |
| **Tests** | Separate functions run against the code to validate that it is operating as intended. | If a test fails after changes, the AI can look at the test output, read what failed, and make the necessary code changes to pass. |

## 4. Advanced Configuration and Workflow Tips

### Custom Rules and Commands
If an AI model makes a mistake multiple times, users can create **custom rules** to codify where the model went wrong and define how it should work in the future.

A powerful feature is defining **custom commands** (e.g., `code review`, `security review`, or `code cleanup review`) that can be run on-demand. These commands use prompts that can include advanced checks (like reviewing authentication changes or ensuring good tests were added).

### Context Management
Users can forward specific context to the agent using the **`@` menu**. This can include files, images, or Git information like the current **branch** (all working changes) or a specific **commit** (one specific change).

**Context Bloat Avoidance:** The quality of the AI's output degrades as the context percentage in a chat increases (especially approaching 80-90%). To avoid this, it is recommended to **make new chats for discrete features** to keep the workflows clean and focused.

### Agent Selection
Cursor provides an **"Auto" model selector** which chooses the best model based on speed, quality, and availability. This is recommended for those new to coding with AI. More advanced users can select specific models, such as a "reasoning model" (like GPT5) for more complex tasks.

## 5. Learning and Non-Coding Use Cases

### Learning to Code
For individuals new to coding, the IDE interface of Cursor—where code structure and syntax are front and center—can be beneficial, as learning often involves **looking at code written by others, decomposing it, and researching its function**.

**Recommended Starter Languages:**
*   **JavaScript:** Recommended because it runs in the web browser, providing immediate visual feedback.
*   **Python:** Recommended because it looks a lot like English, making it easy to read and helping beginners grasp foundational programming concepts (like if/else loops).

### Writing Improvement
The Cursor agent can be utilized outside of traditional coding tasks, such as improving writing style. Users can build a **"mega prompt"** that defines a desired writing style, tone, and specific rules, including a **list of banned words and phrases** (e.g., avoiding "gamechanging," "so innovative," or "we're excited to").

This workflow acts like a "llinter and a formatter" for writing, helping users refine their own drafts to catch generic language or verbal/textual ticks. This is particularly relevant as non-core applications, marketing assets, and internal tooling are increasingly developed via code.

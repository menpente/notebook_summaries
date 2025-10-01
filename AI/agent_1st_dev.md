# Briefing Document: Agent First Development in Fintech

This briefing summarizes key concepts, paradigm shifts, and strategic implications related to Agent First Development (AFD) within the context of PayPal's approach to AI, based on a discussion with Hmonth, a Senior Engineering Manager at PayPal.

## I. Core Definitions

### What is an Agent?
An agent is defined as an entity that possesses the ability to **think and decide** and utilize a set of **tools** within a given context to respond with meaningful information. The ability for models to make calls to specific APIs (tool calling/function calling) and decide what tool to use evolved the technology, leading to standardization efforts like MCP.

### What is Agent First Development (AFD)?
Agent First Development is considered a **paradigm shift** compared to the classic software development cycle.

*   **Core Principle:** The agent is treated as the **first-class citizen**.
*   **Design Approach:** AFD dictates that as systems are designed and their behavior is decided, the agent must be kept as the first-class citizen.
*   **Contrast to Traditional:** It avoids bringing the agent in at the end of the loop, attempting to make a working system "agentic" after it's built.

AFD encompasses two main components:
1.  The **process** in which software is developed using agents.
2.  The **agentic system** developed.

## II. Design Changes and System Traits

### Mental Model Shift in Design
The key difference between traditional and Agent First systems lies in API design and system interaction.

| Traditional System Design | Agent First System Design |
| :--- | :--- |
| Focuses on UI/UX layers, middleware services/APIs, and data sources. | Design APIs specifically to be **consumed by an agent**, not solely by a human using an SDK. |
| Error responses often generic (5xx, 4xx). | Error responses, metadata, and data are **catered to the agent**. Responses can be **more verbose** so the agent knows what action to take next, increasing determinism. |

### Spectrum of Agent Interaction
Agent-first systems exist on a spectrum of autonomy:

| Spectrum Position | Characteristics | Example |
| :--- | :--- | :--- |
| **Left** | Completely **human-driven** interaction. | Human manually searching, selecting size/color, adding to cart, and checking out. |
| **Middle** | **Conversational assistance**. | An agent/bot provides suggestions based on previous transactions or user preferences. |
| **Right (Autonomous)** | **Fully autonomous** where the agent decides and acts. | The agent predicts that a user's shoe is old and orders a replacement, which the user can return if not needed. |

Systems can also involve a **Human in the Loop** (actively providing feedback) or a **Human on the Loop** (monitoring agents to ensure correct behavior).

### Reasoning vs. Thinking
An agent's advanced capabilities extend beyond simple thinking to sophisticated reasoning:

*   **Thinking:** Involves determining necessary steps (e.g., performing API calls) to answer a direct query (e.g., "What's the weather today?").
*   **Reasoning:** Involves integrating context (e.g., calendar, current weather forecast) to predict future needs and provide proactive advice (e.g., "Because the weather is cloudy, you should take an umbrella for your scheduled evening walk").

Autonomous agents can utilize reasoning capabilities to **predict system failures** (such as network bottlenecks or errors) based on historical data, sometimes even before the issue occurs.

## III. Implementation, SDLC, and Skills

### Integrating Agents into Existing Systems
It is unlikely that everything will be replaced by AFD; rather, this paradigm represents the "northstar". Implementation should be selective:

*   **Green Field Projects:** These are easy targets for designing the system with the agent as the first-class citizen.
*   **Existing Systems/Legacy:** Integration should focus on **task-based use cases** where an agent is particularly apt.
*   **Agent Orchestration:** Large companies, like PayPal, can be viewed as an agent itself, containing many internal agents responsible for different domains (e.g., catalog, payment, inventory) that communicate with each other. This minimizes the need to move the entire existing codebase to the agent-first paradigm.

### Impact on Software Development Life Cycle (SDLC)
LLM assistance significantly increases the velocity from **idea to prototype**. However, transitioning from prototype to production still requires finding new patterns due to complex structures, enterprise scale, and legacy systems. Agents can assist throughout the cycle, acting as a "buddy" for design, code generation, and code review.

### New Developer Skills and Mindset
The primary skill developers need is **curiosity**. Developers are encouraged to "get your hands dirty" by experimenting with open-source models, building small projects for fun, and exploring concepts like fine-tuning, datasets, and synthetic data sets.

The mental shift involves moving from converting thoughts into code to training the agent to reflect the developer's process. This requires giving the agent **extensive context** (rules, API documentation, beautiful handwritten code examples) so that the agent becomes a reflection or partner, adding predictability.

### Debugging and Trust
The volume of code generated by LLM assistants is tremendous, requiring sophisticated testing.

*   While LLMs can act as the judge and write test cases, a **human in the loop is still required** to perform reviews based on domain expertise and lessons learned from past production issues.
*   The hypothesis is that starting with an agent-first approach might solve the missing piece required to bridge the gap between prototype and production, addressing the observation that 95% of LLM assistant code currently fails to reach production.

## IV. Opportunities, Challenges, and Future Vision at PayPal

### Strategic Investment at PayPal
PayPal is investing in AFD because it is a **commerce company** connecting millions of merchants and consumers, not just a payments company.

*   **Ecosystem Enhancement:** Agent-first design will enhance the experience for both customers and merchants.
*   **Data Leverage:** PayPal holds historical data from both merchants and consumers that can be used to provide insights, improve profit margins, and enhance commerce journeys.
*   **External Integration:** PayPal views itself as an agent (the "PayPal agent") with expertise in **commerce, payments, risk, compliance, and dispute resolution**. This agent can plug into agentic flows built globally by other entities, using standards like A2A (Agent to Agent).

### Key Challenges and Risks
The biggest challenge is the **rapid pace of evolution** in the AI space—new models, protocols, and patterns are constantly emerging. To address this, systems must be built to be agile:

*   Developers must design systems that allow for **plug-and-play** functionality with new protocols and frameworks.
*   The core of the agent should be **agnostic** to specific frameworks, treating protocols and systems as peripherals.

### Future Vision (3-5 Years)
It is anticipated that **A2A communication and agent orchestrations** will evolve significantly.

*   Agents may develop distinct **personas** (e.g., a "React expert" agent or a "data scientist" agent).
*   A **market of agents** might emerge where users subscribe, assign tasks, and monitor their work.
*   **Agent-First PayPal** is envisioned as a seamless agent that can plug into any global workflow, solving commerce and payment problems regardless of the user's status (PayPal account holder or merchant).

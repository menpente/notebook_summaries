https://www.youtube.com/watch?v=jkon5HsAq30

# Briefing Document: Product Discovery and AI Evals

This briefing summarizes key concepts regarding product discovery, continuous habits, and their essential connection to effective AI evaluations (evals), drawn from discussions with product discovery expert Teresa Torres.

---

## 1. The Importance of Discovery in AI Development

Building AI products is recognized as a hard task, often complicated by external trends, FOMO (Fear Of Missing Out), and pressure to quickly add AI features to roadmaps, which leads to corner-cutting.

The **most critical mistake** AI teams make is picking the wrong customer problem to solve. It is emphasized that **it doesn't matter how good your evals are if you picked the wrong customer problem to solve**.

### Continuous Discovery Habits

Product discovery is defined as the work conducted when deciding *what* to build, contrasted with delivery (the engineering work of writing code and shipping). A crucial observation is that many companies overemphasize delivery and underemphasize discovery, yet both are equally important; a team could build the best version of the wrong product and still fail.

**Continuous Discovery** is defined as: **weekly touch points with customers by the team building the product where they conduct small research activities in pursuit of a desired product outcome**.

This process is grounded in the **scientific method**:

*   Teams start with an **outcome** (e.g., reduce customer churn).
*   They interview customers to learn about their goals and context, developing an **inductive theory** (a hypothesis or mental model of the customer’s world, mapped in the opportunity space).
*   Solutions are designed as **deductive tests** (experiments) of that understanding.
*   When problems arise, the understanding of the opportunity space must be revised.

## 2. Evals as the Next Discovery Habit

Error analysis and eval measuring are viewed as another flavor of the scientific method, ensuring that what is built truly matters to the customer.

Evals are essentially the **next discovery habit** and fall directly into the category of **assumption testing**. Traditional assumption testing evaluates if a solution addresses a customer need and drives a desired outcome. Similarly, evals ask: **Is my solution any good? Is it actually meeting the customer's need?**.

However, the efficacy of evals depends entirely on their foundation: **if your evals aren't grounded in your understanding of customer needs, it's garbage in garbage out**.

### Who is the Benevolent Dictator?

Teams must decide "what good looks like". Instead of letting someone arbitrarily inside the building walls be the "benevolent dictator" of quality, teams should **let the customer be the benevolent dictator**.

Methods for grounding evals in customer reality:

| Evaluation Component | Discovery Best Practices |
| :--- | :--- |
| **Initial Traces & Synthetic Data** | When generating initial traces using synthetic data (based on dimensions like features, personas, and intent), **do not just guess**. The dimensions must be grounded in the discovery foundation, reflecting the opportunities (use cases) the AI will address, the customer segments, and the observed variation in how people express intent. Guessing results in evaluating quality on the wrong data. |
| **Error Analysis** | While some errors are obvious (e.g., suggesting availability when there is none), many errors require **domain knowledge, company strategy knowledge, plus specific customer knowledge** to identify. For tricky or ambiguous cases, showing traces to customers (in a customer-friendly format) and having them annotate them allows for fast feedback loops and lets the customer determine what constitutes an error. |
| **Defining Metrics** | It is important to avoid limiting measurement to generic industry benchmarks or traditional machine learning metrics. Instead, better customer understanding helps define the **right metric**. Off-the-shelf eval tools might be a starting point, but teams must iterate to a custom metric that is **tightly tied to the value their product delivers**. |

## 3. Practical Guidance for AI Product Scoping

### Avoiding the "Ask Me Anything" Trap

A common nightmare scenario is when an AI product features a prompt box that says, "ask me anything". This approach suggests uncertainty about what the product intends to build and makes the user "do all the work".

Good AI teams must make the important decision of **what use cases they are going to cover**.

Recommendations for guiding users and scope:

1.  **Remove the Blank Page Problem:** If the team has a good hypothesis of the feature dimension, they can provide better default text, such as: "Ask me about any of the following things". This steers users toward areas where the AI is designed to be successful.
2.  **Scrubbing Step:** Every successful team interviewed by Torres has a first step in their AI workflow: determining if the intent behind the user input is something the agent can **adequately respond to**. If the input is outside the scope, the agent should respond with something generic (e.g., "connect you with a human") to prevent hallucination.

### Effective Customer Interviews

If behavioral analytics or product instrumentation are lacking (a reality for about 50% of teams surveyed), customer interviews are an essential feedback loop.

To get reliable feedback, teams must avoid asking questions that yield speculative, unreliable, System One responses. **Do not ask customers what they think, what they like, or what they do**.

Instead, teams should: **Ask customers to "Tell me about a specific time when you did a thing"**.

This approach grounds the conversation in a specific story about past behavior, invoking the customer's memory (System Two, the slow, deliberate brain), which yields far more reliable responses. This "look at the data mantra" (observing what happened in reality) is equivalent to the scientific thinking used in evals.

---

## Resources

Teresa Torres is a product discovery coach and the author of the book *Continuous Discovery Habits*.

*   **Podcast:** *Just If Not Possible* – A new podcast where Torres interviews product teams, geeking out on AI architecture, evals, RAG steps, and orchestration.
*   **Blog/Newsletter:** Discovery and AI topics are published at **producttalk.org**.
*   **New Series:** A new series on Claude Code/command line interface tools is available, aiming to teach product managers how to build their own personal operating system for tasks, competitive analysis, and research. (Note: This series includes free conceptual content, with step-by-step instructions gated for supporting members).

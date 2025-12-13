# Briefing: AI-Enhanced Product Management Workflow

## Summary and Context

The role of a Product Manager (PM) is rapidly changing due to the integration of AI tools, enabling PMs to become "AI enhanced," increasing their productivity and impact. PMs who leverage AI will likely replace those who do not. The goal of using these new tools is to accelerate the process of turning "fuzzy ideas into crisp value propositions, road maps, and launch plans".

## AI-Enhanced Product Development Flow

The following workflow demonstrates how AI tools can be leveraged for end-to-end product development, drastically reducing cycle time (the entire process can be completed in approximately 15 to 20 minutes without discussion):

### 1. Market Research and Feature Definition (Approx. 3 Minutes)

The first step for PMs—talking to users and listening to what they want—can be significantly accelerated.

| Step | Tool/Method | Details | Citation |
| :--- | :--- | :--- | :--- |
| **Rapid User Research** | **Perplexity** (using the Discussions filter) | This filter searches through opinions and discussions on platforms like Reddit, allowing PMs to gather the world's opinions on a topic (e.g., interest in a smart fridge) within minutes. References and threads can be reviewed to see the discussion. | |
| **Critical Feature Analysis** | **Perplexity** (Agent Debate Hack) | To obtain high-quality critical thinking, the AI is prompted to create two agents: one *pro* and one *against* the product idea. These agents are instructed to debate (e.g., 20 rounds) based on actual references from the discussion. The outcome is the identification of the **minimum set of features** needed to convince the "against" agent, which helps determine what is required to find product market fit. | |

### 2. PRD Generation (Approx. 90 Seconds)

Once features are identified, the focus shifts to documentation.

| Step | Tool/Method | Details | Citation |
| :--- | :--- | :--- | :--- |
| **Product Document Creation** | **Custom AI Product GBT** | The minimum features from the market research step are pasted into a customized GPT. This GBT is trained with a template of the PM's favorite PRD and can output the document (e.g., problem statement, feature analysis, prioritization) in the PM's specific voice and style. This provides an "incredible head start". | |

### 3. Prototyping and Stakeholder Influence

With the PRD complete, the next step is building and prototyping to bring the vision to life.

| Step | Tool/Method | Details | Citation |
| :--- | :--- | :--- | :--- |
| **UI/Product Prototyping** | **Vzero** (or Google AI Studio) | The completed PRD serves as a high-quality input for these tools, which generate a prototype UI (e.g., a smart fridge dashboard). The extra time spent ensuring the input (the PRD) is good pays off in better prototyping quality. | |
| **Effective Communication** | Prototype Usage | The prototype functions as a critical communication tool that shows the vision "having flesh". Presenting a clickable, functional prototype during product reviews is far more effective than relying solely on a deck based on the PRD, adding credibility and value. | |

### 4. Visualizing Value Proposition

An additional step involves creating visual content to allow others to experience the product idea from the user perspective.

| Step | Tool/Method | Details | Citation |
| :--- | :--- | :--- | :--- |
| **Video Generation** | **Flow** (Google Labs) or **Sora** (OpenAI) | These text-to-video tools generate promotional clips by taking the features or a product narrative from the PRD as input. This visual generation "hammers home the value proposition" and functionality being built. Users can also create "cameos" (AI avatars of themselves) to star in these promotional videos. | |

## Advanced Use Case: AI as a Judge

AI tools can also be used outside of core product development tasks, such as for educational or competitive events.

| Use Case | Tool | Details | Citation |
| :--- | :--- | :--- | :--- |
| **Demo Day Judging** | **Notebook LM** | This tool can function as a judge for pitch competitions or demo days (e.g., for courses or hack weeks). Audio or video recordings of pitches are uploaded. Custom instructions and judging criteria (e.g., innovation, impact, storytelling) are provided, and Notebook LM generates an audio overview announcing winners. The interactive mode allows users to communicate with the AI hosts as if they were live on a radio podcast. | |

## Best Practice Prompting Technique

When generative AI tools fail to produce the desired output, the most effective strategy is to kill the current instance and start over. It is recommended to use AI itself to help write the next prompt, focusing on making the prompt as long and detailed as possible to reduce the need for future iterations.

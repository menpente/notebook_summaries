I'll search for relevant insights about Cursor from Glasp's content before summarizing.The search didn't yield directly relevant insights about the Cursor 201 tutorial content, so I'll proceed with summarizing the transcript without forcing irrelevant citations.

# Cursor 201 - Advanced Techniques Summary

## **Advanced Prompting & Context Engineering** (00:00-12:37)
- **Purpose-based sessions**: Start a new chat session (click "+") for each new focus area to keep context windows focused and improve model accuracy
- **Context window degradation**: Model accuracy decreases as context windows grow larger (per OpenAI research)
- **Multi-tab strategy**: Each tab has its own agent and context window, allowing effective multitasking on discrete tasks while all tabs share real-time codebase awareness
- **Focused prompts**: Submit individual prompts for specific tasks rather than laundry lists—better results with one task per prompt

## **Workflow Features** (13:57-19:17)
- **Steer while working**: Submit prompts while agent is running to add forgotten details—they'll be inserted at the next opportune time
- **Queue prompts**: Hold Option/Alt + Return to queue prompts that execute after current task completes
- **Command automation** (NEW in v1.6): Create markdown files in `cursor/commands/` directory to save reusable commands accessible via "/" slash menu

## **When Models Get Stuck** (19:17-26:46)
- **Strategy 1**: Switch models—different models have different training perspectives even within same lineage
- **Strategy 2**: Ask model to "use chain of thought reasoning and think for 10 paragraphs"—forces deeper thinking and reveals its reasoning process
- **Strategy 3**: Start fresh session—sometimes context window goes "wonky" and needs reset
- **Foundation tip**: Start complex tasks with good context by referencing relevant files/folders, concepts, and even asking questions you know answers to

## **Model Selection Strategy** (27:24-42:18)
- **Standard models**: Daily driver for everyday coding (fastest, cheapest)—examples: Claude 3.5 Sonnet, Claude 4 Sonnet, Gemini 2.5 Pro, GPT-4o
- **Thinking models**: For advanced tasks, planning, specifications, debugging when stuck (slower, more expensive)—examples: Claude 4 Opus, O3
- **Max mode**: For large context needs like codebase audits or extended sessions (200K+ tokens available)—measured in token consumption
- **Auto mode**: Let Cursor pick best model automatically if you don't want to manage selection

## **Long Horizon Tasks** (42:46-1:00:23)
- **Spec + Checklist approach**: 
  1. Use thinking model to create detailed markdown specification through conversation
  2. Generate separate markdown checklist with grouped, sequenced tasks
  3. Reference both files when prompting agent to execute
- **Validation instructions**: Include testing or validation steps in prompt (e.g., "after completing, write and run tests to verify endpoints work")
- **Phase-based execution**: Break large refactors into phases, review after each phase before continuing
- **Benefits**: Agent stays on track, you can monitor progress via checked tasks, easy to resume if interrupted

**Learn more on Glasp:** https://glasp.co/reader?url=https://www.youtube.com/watch?v=PTKFhSfJzFY

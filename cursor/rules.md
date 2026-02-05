Nice choice — Cursor rules are *low-key one of the most powerful parts* of the editor once you get them. I’ll walk you through it step by step, no assumed knowledge, and we’ll keep it practical.

---

## What “rules” mean in Cursor (plain English)

**Rules tell Cursor’s AI how to behave *for your project*.**
They’re like permanent instructions the AI follows every time it helps you.

Examples:

* “Always use TypeScript, never JavaScript”
* “Follow our company’s React patterns”
* “Don’t suggest changes outside the file I’m editing”
* “Use functional programming, no classes”

Instead of repeating yourself in every prompt, you set rules once.

---

## Where Cursor rules live

Cursor uses a special file:

```
.cursor/rules.md
```

This file:

* Is **checked into your repo**
* Applies to **everyone** using Cursor on the project
* Is read automatically by the AI

If the folder/file doesn’t exist yet, you create it.

---

## How to create your first rules file

1. Open your project in Cursor
2. In the file explorer:

   * Create a folder called `.cursor`
   * Inside it, create a file called `rules.md`

Your structure should look like:

```
your-project/
  .cursor/
    rules.md
```

That’s it — Cursor will pick it up automatically.

---

## Basic rules.md example (start here)

Paste this into `rules.md`:

```md
# Cursor Rules

## General
- Prefer simple, readable solutions over clever ones
- Explain reasoning briefly when suggesting changes

## Code Style
- Use TypeScript
- Use async/await instead of promises
- Prefer functional components over class components

## Safety
- Do not modify files unless explicitly asked
- Do not introduce new dependencies without asking
```

This already changes how Cursor behaves **everywhere** in your repo.

---

## How Cursor actually uses these rules

Whenever you:

* Ask a question in the chat
* Highlight code and press `Cmd + K`
* Ask Cursor to refactor, explain, or generate code

Cursor silently:

1. Reads your `rules.md`
2. Merges it with your prompt
3. Generates answers that follow those constraints

You don’t have to mention the rules again.

---

## Writing *good* rules (this matters)

### ✅ Be specific

Bad:

```md
- Write good code
```

Good:

```md
- Use early returns instead of nested conditionals
```

---

### ✅ Use “Do / Don’t” language

Cursor responds well to clear constraints.

```md
- Do not use default exports
- Always use named exports
```

---

### ✅ Group rules by intent

Cursor understands structure surprisingly well.

```md
## Testing
- Use Jest
- Prefer integration tests over unit tests

## Formatting
- Max line length: 100 characters
- Use trailing commas
```

---

## Advanced: contextual rules (pro tip)

You can give **conditional behavior**:

```md
## React Files
- When editing React components:
  - Use hooks only
  - Avoid useEffect unless necessary

## Backend Code
- When editing backend services:
  - Validate all inputs
  - Prefer explicit error handling
```

Cursor is good at inferring context from filenames and folders.

---

## Common mistakes to avoid

❌ Treating rules like comments
→ They are **instructions**, not documentation

❌ Making them too vague
→ The AI can’t enforce “clean architecture” unless you define what that means

❌ Overloading rules with everything
→ Start small; add rules when you notice repeated annoyances

---

## How I recommend learning rules (fastest path)

1. Start with **5–10 rules**
2. Use Cursor for a day
3. Notice:

   * “Why did it do *that*?”
   * “Why didn’t it do *this*?”
4. Add a rule to fix it
5. Repeat

Your rules file becomes a **memory + standards doc** for the AI.

---

## Want to go further?

If you want, I can:

* Help you **write rules for your exact stack** (React, backend, infra, etc.)
* Review a rules file you already have
* Show **real examples** where rules dramatically change Cursor’s output
* Help you design **team-wide rules vs personal rules**

Tell me:
👉 *What kind of project are you using Cursor for right now?*

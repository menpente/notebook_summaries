# Skill Creation Cliff Notes

## What is a Skill?

A modular package that extends Claude's capabilities with specialized knowledge, workflows, and tools. Think of it as an "onboarding guide" for specific tasks.

## Quick Start

```bash
# 1. Create new skill
skill-creator/scripts/init_skill.py my-skill-name --path ./

# 2. Edit SKILL.md and add resources
# 3. Validate
skill-creator/scripts/quick_validate.py my-skill-name/

# 4. Package
skill-creator/scripts/package_skill.py my-skill-name/
```

## Skill Structure

```
my-skill/
├── SKILL.md (required)
├── scripts/         (optional - executable code)
├── references/      (optional - docs loaded as needed)
└── assets/          (optional - files used in output)
```

## SKILL.md Format

```markdown
---
name: my-skill-name
description: Complete explanation of what skill does and WHEN to use it
license: Apache 2.0 (optional)
---

# My Skill Name

[Instructions in imperative form: "Do X" not "You should do X"]

## When to Use
- Specific scenario 1
- Specific scenario 2

## How to Use
[Reference bundled resources and explain workflow]
```

## Bundled Resources

| Directory      | Purpose | When to Use | Example |
|---------------|---------|-------------|---------|
| **scripts/** | Executable code | Deterministic tasks, repeatedly-rewritten code | `rotate_pdf.py` |
| **references/** | Documentation | Schemas, APIs, policies loaded as needed | `api_docs.md`, `schema.md` |
| **assets/** | Output files | Templates, images, boilerplate code | `logo.png`, `template.pptx` |

## Writing Guidelines

### YAML Frontmatter
- `name`: Lowercase, hyphens only (must match directory name)
- `description`: Be specific about WHEN to use the skill, include trigger scenarios

### Markdown Body
- **Use imperative/infinitive form**: "To do X, run Y" ✓
- **Avoid second person**: "You should run Y" ✗
- **Keep it lean**: Move detailed docs to `references/`
- **Focus on procedural knowledge**: What's non-obvious to Claude?

## The 6-Step Process

1. **Understand with Examples** - Get concrete use cases from users
2. **Plan Contents** - Identify needed scripts, references, assets
3. **Initialize** - Run `init_skill.py` to create template
4. **Edit** - Write SKILL.md, add resources, delete unused examples
5. **Package** - Validate and create distributable zip
6. **Iterate** - Test on real tasks, improve based on feedback

## Progressive Disclosure

Skills load information in 3 levels to manage context:
1. **Metadata** (~100 words) - Always loaded
2. **SKILL.md body** (<5k words) - Loaded when triggered
3. **Resources** (unlimited) - Loaded/executed as needed

## Key Principles

- **Build for workflows, not API endpoints** - Enable complete tasks
- **Optimize for context** - Return high-signal info, not data dumps
- **Actionable errors** - Guide Claude toward correct usage
- **Natural subdivisions** - Design around how humans think about tasks
- **No duplication** - Info lives in SKILL.md OR references, not both

## Common Patterns

### For File Processing (PDF, Excel, etc.)
- Scripts for deterministic operations (rotate, merge, extract)
- References for format specifications
- Assets for templates or sample files

### For API Integration (BigQuery, Slack, etc.)
- Scripts for repetitive API operations
- References for schemas, endpoints, auth patterns
- No assets typically needed

### For Creative Tasks (Design, Art, etc.)
- Few/no scripts (Claude generates code)
- References for style guides, design principles
- Assets for templates, fonts, brand resources

### For Workflows (Communications, Testing, etc.)
- Scripts for automation steps
- References for policies, standards, examples
- Assets for templates and boilerplate

## Validation Checklist

- [ ] SKILL.md exists with proper frontmatter
- [ ] `name` matches directory name (hyphen-case)
- [ ] `description` explains what AND when
- [ ] Instructions use imperative form
- [ ] Bundled resources are referenced in SKILL.md
- [ ] Unused example files deleted
- [ ] Passes `quick_validate.py`
- [ ] Tested on real use cases

## Quick Tips

- Start with concrete examples before building
- Delete unused directories from template
- Keep SKILL.md under 5k words
- Test the skill by using it immediately after creation
- Iterate based on actual usage, not speculation

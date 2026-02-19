---
name: capture-lesson
description: Persists a learning to tasks/lessons.md after user corrections. Use automatically WHENEVER the user corrects something, points out a mistake, or asks not to repeat a behavior.
context: fork
agent: general-purpose
disable-model-invocation: false
allowed-tools: Read, Write
---

## Task

Record the following learning in `tasks/lessons.md`:

**Correction received:** $ARGUMENTS

## Instructions

1. Read the file `tasks/lessons.md` (create it if it doesn't exist)
2. Check if a similar lesson already exists — if so, update it instead of duplicating
3. Add the new lesson in the format below
4. Save the file

## Entry Format

```markdown
### [CATEGORY] - Short lesson title

**Pattern identified:** Description of the incorrect error or behavior
**Rule:** What to do instead
**Trigger:** When this rule should be applied
**Recorded on:** YYYY-MM-DD
```

## Available Categories

- `[ARCHITECTURE]` — Design and structure decisions
- `[CODE]` — Implementation patterns
- `[COMMUNICATION]` — Tone, verbosity, response format
- `[PROCESS]` — Workflow, verification, planning
- `[TOOLS]` — CLI, API, framework usage
- `[PROJECT]` — Rules specific to the current project

## Rules

- Be specific: capture the pattern, not the isolated case
- One lesson = one clear, actionable rule
- Maximum 4 lines per lesson
- Never remove existing lessons without explicit reason
- Return to the main context only with: "Lesson recorded: [title]"

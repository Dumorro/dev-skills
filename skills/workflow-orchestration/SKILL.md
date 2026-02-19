---
name: workflow-orchestration
description: Activates the full Workflow Orchestration protocol with plan mode, subagent strategy, self-improvement loop, verification, elegance, and autonomous bug fixing. Use when starting any non-trivial task (3+ steps), architectural decisions, or when receiving a bug report.
disable-model-invocation: false
---

## Workflow Orchestration Protocol

### 1. Plan Mode Default
- Enter plan mode for ANY non-trivial task (3+ steps or architectural decisions)
- If something goes wrong, STOP and replan immediately — don't keep pushing
- Use plan mode for verification steps, not just for building
- Write detailed specs upfront to reduce ambiguity

### 2. Subagent Strategy
- Use subagents liberally to keep the main context window clean
- Delegate research, exploration, and parallel analysis to subagents
- For complex problems, use more compute via subagents
- One task per subagent for focused execution

### 3. Self-Improvement Loop
- After ANY user correction: invoke `/capture-lesson [description of the correction]` via subagent
- Write rules for yourself that prevent the same mistake
- Iterate ruthlessly on those lessons until the error rate drops
- Review lessons at the start of each session for the relevant project

### 4. Verification Before Done
- Never mark a task as complete without proving it works
- Diff behavior between main and your changes when relevant
- Ask yourself: "Would a staff engineer approve this?"
- Run tests, check logs, demonstrate correctness

### 5. Demand Elegance (Balanced)
- For non-trivial changes: pause and ask "Is there a more elegant way?"
- If a fix feels hacky: "Knowing everything I know now, implement the elegant solution"
- Skip this for simple, obvious fixes — don't over-engineer
- Challenge your own work before presenting it

### 6. Autonomous Bug Fixing
- When receiving a bug report: just fix it. Don't ask for guidance
- Point to logs, errors, failing tests — then resolve
- Zero context switching required from the user
- Fix failing CI tests without needing to be told how

---

## Task Management Protocol

Follow this flow for every task:

1. **Plan First**: Write the plan in `tasks/todo.md` with checkable items
2. **Verify Plan**: Confirm before starting implementation
3. **Track Progress**: Mark items as complete as you progress
4. **Explain Changes**: High-level summary at each step
5. **Document Results**: Add a review section in `tasks/todo.md`
6. **Capture Lessons**: Update `tasks/lessons.md` after corrections

---

## Core Principles

- **Simplicity First**: Make each change as simple as possible. Minimal code impact
- **No Laziness**: Find root causes. No temporary fixes. Senior developer standard
- **Minimal Impact**: Changes should touch only what's necessary. Avoid introducing bugs

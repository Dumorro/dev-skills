# dev-skills

Custom skills for [Claude Code](https://docs.anthropic.com/en/docs/claude-code) — workflow orchestration, self-improvement, and code analysis.

## Skills

| Skill | Description | Activation |
|-------|-------------|------------|
| **workflow-orchestration** | Plan mode, subagent strategy, verification, and autonomous bug fixing | Non-trivial tasks (3+ steps), architecture decisions, bug reports |
| **capture-lesson** | Persists learnings to `tasks/lessons.md` after corrections | Automatic when the user corrects a mistake |
| **big-o-analyzer** | Time/space complexity analysis with optimization suggestions | Algorithms, loops, sorting, searching, performance reviews |
| **asymptotic-analyzer** | Rigorous asymptotic analysis: O/Ω/Θ/o/ω notation, Master Theorem, amortized analysis | Recursive functions, formal complexity proofs, system design, performance-critical code |

## Installation

### 1. Clone

```bash
git clone https://github.com/dumorro/dev-skills.git
```

### 2. Copy to your project

```bash
# All skills
cp -r dev-skills/skills/* your-project/.claude/skills/

# Single skill
cp -r dev-skills/skills/big-o-analyzer your-project/.claude/skills/
cp -r dev-skills/skills/asymptotic-analyzer your-project/.claude/skills/
```

### 3. Use

Skills activate automatically based on context, or via slash commands:

```
/workflow-orchestration Refactor the authentication module
/capture-lesson Always use parameterized queries instead of string interpolation
/big-o-analyzer src/utils/search.ts:binarySearch
```

## Structure

```
skills/
  big-o-analyzer/
    SKILL.md              # Skill definition and analysis rules
    reference.md          # Big O cheat sheet
    patterns.md           # Common anti-patterns and fixes
    examples/
      analysis.md         # Real-world analysis examples
  asymptotic-analyzer/
    SKILL.md              # Skill definition and analysis protocol
    notation.md           # Formal definitions: O, Ω, Θ, o, ω
    master-theorem.md     # Master Theorem, Akra-Bazzi, recursion trees
    amortized.md          # Aggregate, accounting, potential methods
    examples/
      full-analysis.md    # Merge sort, QuickSort, binary search, dynamic array
  capture-lesson/
    SKILL.md
  workflow-orchestration/
    SKILL.md
```

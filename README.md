# dev-skills

Claude Code custom skills for workflow orchestration, self-improvement, and code analysis.

## Available Skills

| Skill | Description |
|-------|-------------|
| **workflow-orchestration** | Full workflow protocol with plan mode, subagent strategy, verification, and autonomous bug fixing |
| **capture-lesson** | Automatically persists learnings after user corrections to `tasks/lessons.md` |
| **big-o-analyzer** | Analyzes time and space complexity (Big-O) of code with optimization suggestions |

## Installation

### 1. Clone the repo

```bash
git clone https://github.com/dumorro/dev-skills.git
```

### 2. Copy skills to your project

Copy the skills you want into your project's `.claude/skills/` directory:

```bash
# All skills
cp -r dev-skills/skills/*/ your-project/.claude/skills/

# Or a single skill
cp -r dev-skills/skills/big-o-analyzer your-project/.claude/skills/
```

### 3. Verify installation

Skills are available once they exist in `.claude/skills/` within your project. You can invoke them with slash commands in Claude Code:

```
/workflow-orchestration
/capture-lesson <description>
/big-o-analyzer <file:function>
```

## Usage Examples

```
/big-o-analyzer src/utils/search.ts:binarySearch
/capture-lesson Always use parameterized queries instead of string interpolation
/workflow-orchestration Refactor the authentication module
```

## Structure

```
skills/
  big-o-analyzer/
    SKILL.md
  capture-lesson/
    SKILL.md
  workflow-orchestration/
    SKILL.md
```

---
name: big-o-analyzer
description: Analyzes code for time and space complexity (Big-O notation). Use when the user asks about performance, complexity analysis, or optimization of algorithms and data structures.
context: fork
agent: general-purpose
disable-model-invocation: false
allowed-tools: Read, Grep, Glob
---

## Task

Analyze the time and space complexity of the provided code or function:

**Target:** $ARGUMENTS

## Instructions

1. Identify the target code — read the file/function specified
2. Trace all loops, recursive calls, and data structure operations
3. Determine the time complexity (best, average, worst case)
4. Determine the space complexity (auxiliary space)
5. Identify any hidden costs (e.g., string concatenation, sorting within loops, hash collisions)
6. Suggest optimizations if complexity can be improved

## Output Format

```markdown
### Complexity Analysis: [function/method name]

**Time Complexity:**
- Best case: O(?)
- Average case: O(?)
- Worst case: O(?)

**Space Complexity:** O(?) auxiliary

**Breakdown:**
- [Line/block reference]: [explanation of contribution to complexity]

**Hidden Costs:**
- [Any non-obvious performance implications]

**Optimization Opportunities:**
- [Suggested improvements with expected complexity gains, or "None — already optimal"]
```

## Rules

- Always specify what n represents (e.g., array length, number of nodes)
- Account for built-in method costs (e.g., `Array.sort` is O(n log n), `Array.includes` is O(n))
- Flag amortized vs worst-case distinctions where relevant
- If multiple variables affect complexity, use multi-variable notation (e.g., O(n * m))
- Be precise — O(n) and O(2n) are both O(n), but mention constant factors if they matter practically
- Return to main context with: "Complexity analysis complete: [summary]"

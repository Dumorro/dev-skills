# Recurrence Relations and the Master Theorem

## The Master Theorem

For recurrences of the form:
```
T(n) = a·T(n/b) + f(n)
```

Where:
- `a ≥ 1` — number of subproblems
- `b > 1` — factor by which input shrinks
- `f(n)` — cost of work done outside recursive calls

Define the **critical exponent**: `c* = log_b(a)`

---

### Case 1: f(n) = O(n^(c*-ε)) for some ε > 0
**Condition**: f(n) grows *polynomially slower* than n^c*
**Solution**: `T(n) = Θ(n^c*)`
**Intuition**: Recursive calls dominate the work.

**Example**: T(n) = 8T(n/2) + O(n²)
```
c* = log₂8 = 3; f(n) = O(n²) = O(n^(3-1)) → Case 1
T(n) = Θ(n³)
```

---

### Case 2: f(n) = Θ(n^c* · log^k(n)) for k ≥ 0
**Condition**: f(n) grows at the *same rate* as n^c* (possibly × polylog)
**Solution**: `T(n) = Θ(n^c* · log^(k+1)(n))`
**Intuition**: Each level contributes equally.

**Example (k=0)**: T(n) = 2T(n/2) + O(n)
```
c* = log₂2 = 1; f(n) = Θ(n¹·log⁰n) → Case 2 (k=0)
T(n) = Θ(n log n)  ← Merge Sort
```

**Example (k=1)**: T(n) = 2T(n/2) + O(n log n)
```
c* = 1; f(n) = Θ(n log n) → Case 2 (k=1)
T(n) = Θ(n log² n)
```

---

### Case 3: f(n) = Ω(n^(c*+ε)) for some ε > 0, and regularity holds
**Condition**: f(n) grows *polynomially faster* than n^c*
**Regularity condition**: `a·f(n/b) ≤ c·f(n)` for some c < 1
**Solution**: `T(n) = Θ(f(n))`
**Intuition**: The work at the root dominates.

**Example**: T(n) = 2T(n/2) + O(n²)
```
c* = log₂2 = 1; f(n) = Ω(n^(1+1)) → Case 3
T(n) = Θ(n²)
```

---

## Common Recurrences Cheat Sheet

| Recurrence                       | Algorithm               | Result        |
|----------------------------------|-------------------------|---------------|
| T(n) = T(n/2) + O(1)             | Binary Search           | Θ(log n)      |
| T(n) = 2T(n/2) + O(1)            | Tree Traversal          | Θ(n)          |
| T(n) = 2T(n/2) + O(n)            | Merge Sort              | Θ(n log n)    |
| T(n) = 4T(n/2) + O(n)            | —                       | Θ(n²)         |
| T(n) = 4T(n/2) + O(n²)           | —                       | Θ(n² log n)   |
| T(n) = 8T(n/2) + O(n²)           | Matrix Multiply (naive) | Θ(n³)         |
| T(n) = 7T(n/2) + O(n²)           | Strassen                | Θ(n^2.807)    |
| T(n) = T(n-1) + O(1)             | Factorial               | Θ(n)          |
| T(n) = T(n-1) + O(n)             | Selection Sort          | Θ(n²)         |
| T(n) = 2T(n-1) + O(1)            | Naive Fibonacci         | Θ(2ⁿ)         |
| T(n) = T(n/3) + T(2n/3) + O(n)   | QuickSort (bad pivot)   | Θ(n log n)    |
| T(n) = 9T(n/3) + O(n)            | —                       | Θ(n²)         |

---

## When Master Theorem DOESN'T Apply

Use alternative methods when:
- f(n) is not polynomially bounded (e.g., f(n) = n/log n)
- Subproblems have unequal sizes (e.g., T(n) = T(n/3) + T(2n/3) + n)
- `a` or `b` are not constants

### Alternative: Akra-Bazzi Method

For `T(n) = Σᵢ aᵢT(n/bᵢ) + f(n)`:

1. Find `p` such that `Σᵢ aᵢ/bᵢᵖ = 1`
2. `T(n) = Θ(nᵖ(1 + ∫₁ⁿ f(u)/u^(p+1) du))`

**Example**: T(n) = T(n/3) + T(2n/3) + n
```
Solve: (1/3)ᵖ + (2/3)ᵖ = 1 → p = 1
∫₁ⁿ u/u² du = ln(n)
T(n) = Θ(n log n) ✓
```

### Alternative: Substitution Method (Proof by Induction)

1. **Guess** a solution form (use recursion tree to guide the guess)
2. **Substitute** into the recurrence
3. **Prove** by induction that T(n) ≤ c·f(n) for appropriate c and n₀

---

## Recursion Tree Method

Visualize the recurrence to guess the closed form:
1. Draw the first 3-4 levels of recursion
2. Sum cost per level
3. Count total number of levels
4. Sum over all levels

**Example**: T(n) = 2T(n/2) + n
```
Level 0:   1 node  × n         cost: n
Level 1:   2 nodes × (n/2)     cost: n
Level 2:   4 nodes × (n/4)     cost: n
...
Level k:   2ᵏ nodes × (n/2ᵏ)  cost: n
...
Level log n: n leaves × O(1)   cost: n

Total levels: log₂n + 1
Total cost:   n × (log n + 1) = Θ(n log n)
```

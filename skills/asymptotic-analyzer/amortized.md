# Amortized Analysis

Amortized analysis determines the average cost per operation in a
**sequence** of operations — even when individual operations vary wildly in cost.

> Key insight: An expensive operation must have been preceded by many cheap
> operations that "saved up" for it. The true per-operation cost is amortized
> across the sequence.

## When to Apply Amortized Analysis

- Dynamic array (`List<T>`, `ArrayList`, `Vec`) push with occasional resize
- Hash table with periodic rehashing
- Stack with multi-pop (pop k elements at once)
- Splay trees, skew heaps, Fibonacci heaps
- Any structure where occasional O(n) ops are paid for by O(1) preceding ops

---

## Method 1: Aggregate Method

**How it works**:
1. Compute T(n) = total cost of n operations in the worst case
2. Amortized cost per operation = T(n) / n

**Classic example: Dynamic Array Push**

Let a dynamic array double when full:
```
- n pushes where array starts at size 1
- Resize costs: 1 + 2 + 4 + 8 + ... + n = 2n - 1  (geometric sum)
- n regular push costs: n × O(1) = n
- Total: T(n) = n + (2n - 1) ≈ 3n = O(n)
- Amortized cost per push: O(n)/n = O(1) ✓
```

---

## Method 2: Accounting Method (Banker's Method)

**How it works**:
1. Assign an **amortized cost** (credit) to each operation
2. Credits paid upfront cover future expensive operations
3. Ensure the credit balance never goes negative

**Invariant**: `Σ (amortized cost) ≥ Σ (actual cost)`

**Classic example: Dynamic Array Push**

Assign each push an amortized cost of 3 units:
```
- 1 unit: pays for the actual push
- 1 unit: saved for copying this element during the NEXT resize
- 1 unit: saved for copying an OLD element during the next resize

When resize occurs (array has n elements, costs n copies):
  → Each of the n elements has 1 saved credit → exactly pays for its copy
  → Balance never goes negative
  → Amortized cost per push: O(1) ✓
```

---

## Method 3: Potential Method (Physicist's Method)

**How it works**:
1. Define a **potential function** Φ(Dᵢ) over the data structure state Dᵢ
2. Amortized cost of operation i: `âᵢ = cᵢ + Φ(Dᵢ) - Φ(Dᵢ₋₁)`
3. Total actual cost: `Σ cᵢ = Σ âᵢ - (Φ(Dₙ) - Φ(D₀))`
4. If `Φ(Dₙ) ≥ Φ(D₀)`, then `Σ cᵢ ≤ Σ âᵢ`

**Classic example: Dynamic Array Push**

Define `Φ(D) = 2 × (current size) - (current capacity)`
```
- When array is half-full: Φ = 2(n/2) - n = 0
- When array is full:      Φ = 2n - n = n

Regular push (no resize):
  actual cost cᵢ = 1
  ΔΦ = 2(k+1) - cap - (2k - cap) = 2
  âᵢ = 1 + 2 = 3 = O(1)

Resize push (array doubles from n to 2n):
  actual cost cᵢ = n + 1  (copy all + push)
  ΔΦ = 2(n+1) - 2n - (2n - n) = 2 - n
  âᵢ = (n+1) + (2-n) = 3 = O(1)

Amortized cost per push: O(1) ✓
```

---

## Comparison of Methods

| Method     | Technique                   | Best Used When                       |
|------------|-----------------------------|--------------------------------------|
| Aggregate  | Total / n                   | Simple, uniform sequences            |
| Accounting | Assign prepaid credits      | Easy to reason about credits         |
| Potential  | Φ(state) function           | Complex structures, formal proofs    |

---

## Common Amortized Results

| Structure / Operation               | Amortized Cost  | Method     |
|-------------------------------------|-----------------|------------|
| Dynamic array push                  | O(1)            | All three  |
| Dynamic array pop                   | O(1)            | —          |
| Hash table insert (with rehash)     | O(1)            | Aggregate  |
| Splay tree find/insert              | O(log n)        | Potential  |
| Fibonacci heap insert               | O(1)            | Potential  |
| Fibonacci heap extract-min          | O(log n)        | Potential  |
| Disjoint set union (path compress)  | O(α(n)) ≈ O(1) | Potential  |
| Multi-pop stack (k elements)        | O(1) per push   | Accounting |

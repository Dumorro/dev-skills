# Asymptotic Notation Reference

## Formal Definitions

### Big O — O(f(n)) — Upper Bound
> "f(n) is an asymptotic upper bound for T(n)"

```
T(n) = O(f(n)) iff:
∃ c > 0 and n₀ > 0 such that ∀ n ≥ n₀: T(n) ≤ c · f(n)
```

**Meaning**: T(n) grows *at most* as fast as f(n) for large n.
**Use for**: Worst-case guarantees. The most common notation.

---

### Big Omega — Ω(f(n)) — Lower Bound
> "f(n) is an asymptotic lower bound for T(n)"

```
T(n) = Ω(f(n)) iff:
∃ c > 0 and n₀ > 0 such that ∀ n ≥ n₀: T(n) ≥ c · f(n)
```

**Meaning**: T(n) grows *at least* as fast as f(n) for large n.
**Use for**: Best-case guarantees and algorithm lower-bound proofs.

---

### Big Theta — Θ(f(n)) — Tight Bound
> "f(n) is an asymptotically tight bound for T(n)"

```
T(n) = Θ(f(n)) iff:
T(n) = O(f(n))  AND  T(n) = Ω(f(n))
i.e., ∃ c₁, c₂ > 0 and n₀ > 0 such that ∀ n ≥ n₀:
  c₁ · f(n) ≤ T(n) ≤ c₂ · f(n)
```

**Meaning**: T(n) grows *exactly* at the rate of f(n).
**Use for**: When you can prove both bounds match. This is the strongest statement.

---

### Little o — o(f(n)) — Strict Upper Bound
> "f(n) strictly dominates T(n)"

```
T(n) = o(f(n)) iff:
lim(n→∞) T(n)/f(n) = 0
```

**Meaning**: T(n) grows *strictly slower* than f(n).
**Examples**: n = o(n²), log n = o(n), n⁰·⁹⁹⁹ = o(n)
**Use for**: Proving an algorithm is strictly better than a bound.

---

### Little Omega — ω(f(n)) — Strict Lower Bound
> "T(n) strictly dominates f(n)"

```
T(n) = ω(f(n)) iff:
lim(n→∞) T(n)/f(n) = ∞
```

**Meaning**: T(n) grows *strictly faster* than f(n).
**Examples**: n² = ω(n), n log n = ω(n)
**Use for**: Proving a lower bound is strict.

---

## Notation Comparison Table

| Notation | Intuitive Analogy | Formal Condition           | Example          |
|----------|-------------------|----------------------------|------------------|
| O(f)     | T ≤ f (roughly)   | T/f bounded above          | 3n² = O(n²)      |
| Ω(f)     | T ≥ f (roughly)   | T/f bounded below          | 3n² = Ω(n)       |
| Θ(f)     | T = f (roughly)   | T/f bounded above and below| 3n² = Θ(n²)      |
| o(f)     | T < f (strictly)  | T/f → 0                   | n = o(n²)        |
| ω(f)     | T > f (strictly)  | T/f → ∞                   | n² = ω(n)        |

## Common Complexity Classes (Ordered)

```
O(1) ⊂ O(log log n) ⊂ O(log n) ⊂ O(√n) ⊂ O(n) ⊂ O(n log n)
     ⊂ O(n²) ⊂ O(n³) ⊂ O(nᵏ) ⊂ O(2ⁿ) ⊂ O(n!) ⊂ O(nⁿ)
```

## Simplification Rules

When determining O/Θ, apply these rules:
1. **Drop constants**: O(3n) → O(n), O(n/2) → O(n)
2. **Drop lower-order terms**: O(n² + n) → O(n²)
3. **Dominant term wins**: O(n³ + n! + 2ⁿ) → O(n!)
4. **Log base doesn't matter**: O(log₂ n) = O(log₁₀ n) = O(log n)
5. **Polynomial vs exponential**: nᵏ = o(aⁿ) for any k ≥ 1, a > 1
6. **Poly-log vs polynomial**: (log n)ᵏ = o(n^ε) for any ε > 0

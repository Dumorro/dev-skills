# Full Asymptotic Analysis Examples

## Example 1: Merge Sort

```typescript
function mergeSort(arr: number[]): number[] {
  if (arr.length <= 1) return arr;
  const mid = Math.floor(arr.length / 2);
  const left = mergeSort(arr.slice(0, mid));   // T(n/2)
  const right = mergeSort(arr.slice(mid));      // T(n/2)
  return merge(left, right);                    // O(n)
}
```

**Recurrence**: T(n) = 2T(n/2) + O(n)

**Master Theorem**:
- a = 2, b = 2 → c* = log₂2 = 1
- f(n) = O(n) = O(n¹)
- f(n) = Θ(n^c* · log⁰n) → **Case 2** (k=0)
- **T(n) = Θ(n log n)**

```
/**
 * ═══════════════════════════════════════════
 * ASYMPTOTIC ANALYSIS — Merge Sort
 * ═══════════════════════════════════════════
 * Time Complexity:
 *   Best case:    Ω(n log n) — always divides and merges
 *   Average case: Θ(n log n) — uniform input distribution
 *   Worst case:   O(n log n) — always n log n regardless of input
 *   Tight bound:  Θ(n log n) — O = Ω confirmed ✓
 *   Amortized:    N/A (not a repeated-operation structure)
 *
 * Space Complexity:
 *   Auxiliary:    O(n)      — merge step needs temporary arrays
 *   Stack depth:  O(log n)  — recursion depth = log₂n levels
 *   Total:        O(n)
 *
 * Recurrence:
 *   T(n) = 2T(n/2) + O(n)
 *   Master Theorem: Case 2 (k=0) → T(n) = Θ(n log n)
 *
 * Bottleneck: merge() at each level — Θ(n) work × log n levels
 * Tight bound confirmed: Yes — best and worst are both n log n
 * ═══════════════════════════════════════════
 */
```

---

## Example 2: QuickSort (Average Case Analysis)

**Recurrence for average case** (random pivot):
```
T(n) = T(k) + T(n-k-1) + O(n),  k uniform over [0, n-1]

Expected value:
E[T(n)] = (2/n) Σₖ₌₀ⁿ⁻¹ E[T(k)] + O(n)
→ solves to E[T(n)] = Θ(n log n)  via substitution method
```

**Worst case** (sorted array, last element as pivot):
```
T(n) = T(n-1) + O(n) → T(n) = O(n²)
```

```
/**
 * ═══════════════════════════════════════════
 * ASYMPTOTIC ANALYSIS — QuickSort
 * ═══════════════════════════════════════════
 * Time Complexity:
 *   Best case:    Ω(n log n) — pivot always splits evenly
 *   Average case: Θ(n log n) — random pivot, uniform distribution
 *   Worst case:   O(n²)      — sorted input, bad pivot selection
 *   Tight bound:  NOT Θ(n log n) — O ≠ Ω in worst-case sense
 *   Amortized:    N/A
 *
 * Space Complexity:
 *   Auxiliary:    O(1)             — in-place partitioning
 *   Stack depth:  O(log n) avg /
 *                 O(n) worst       — recursion depth
 *   Total:        O(log n) avg, O(n) worst
 *
 * Recurrence:
 *   Best:    T(n) = 2T(n/2) + O(n) → Θ(n log n) [Master Case 2]
 *   Worst:   T(n) = T(n-1) + O(n)  → O(n²)       [telescoping]
 *   Average: E[T(n)] = Θ(n log n)  [probabilistic analysis]
 *
 * Bottleneck: Partition quality — unbalanced splits degrade to O(n²)
 * Tight bound confirmed: No — worst case is O(n²), not O(n log n)
 * Mitigation: Random pivot or median-of-3 → expected Θ(n log n)
 * ═══════════════════════════════════════════
 */
```

---

## Example 3: Binary Search (Iterative)

```typescript
function binarySearch(arr: number[], target: number): number {
  let lo = 0, hi = arr.length - 1;
  while (lo <= hi) {                 // O(log n) iterations
    const mid = (lo + hi) >> 1;
    if (arr[mid] === target) return mid;
    if (arr[mid] < target) lo = mid + 1;
    else hi = mid - 1;
  }
  return -1;
}
```

**Recurrence**: T(n) = T(n/2) + O(1)
**Master Theorem**: a=1, b=2, c*=log₂1=0, f(n)=O(1)=O(n⁰) → Case 2 (k=0)
**T(n) = Θ(log n)**

```
/**
 * ═══════════════════════════════════════════
 * ASYMPTOTIC ANALYSIS — Binary Search
 * ═══════════════════════════════════════════
 * Time Complexity:
 *   Best case:    Ω(1)       — target is the middle element
 *   Average case: Θ(log n)   — expected ≈ log n comparisons
 *   Worst case:   O(log n)   — target not found or at boundary
 *   Tight bound:  NOT Θ(log n) overall (best case is Ω(1))
 *
 * Space Complexity:
 *   Auxiliary:    O(1) — only lo, hi, mid variables
 *   Stack depth:  O(1) — iterative, no recursion
 *   Total:        O(1)
 *
 * Recurrence (recursive version):
 *   T(n) = T(n/2) + O(1)
 *   Master Theorem: Case 2 (k=0, c*=0) → T(n) = Θ(log n)
 *
 * Bottleneck: The halving loop — log₂n iterations maximum
 * Tight bound confirmed: For worst/average case only (Θ(log n))
 *   Full range: Ω(1) ≤ T(n) ≤ O(log n)
 * ═══════════════════════════════════════════
 */
```

---

## Example 4: Dynamic Array Push (Amortized)

```csharp
// C# List<T>.Add() — backed by T[] that doubles on overflow
var list = new List<int>();       // capacity = 4 (default)
for (int i = 0; i < n; i++) {
    list.Add(i);                  // amortized O(1)
}
```

```
/**
 * ═══════════════════════════════════════════
 * ASYMPTOTIC ANALYSIS — List<T>.Add (n calls)
 * ═══════════════════════════════════════════
 * Time Complexity (single Add):
 *   Best case:    Ω(1) — no resize needed
 *   Worst case:   O(n) — resize from n to 2n copies n elements
 *   Amortized:    O(1) — aggregate method:
 *                        total cost for n adds
 *                        = n (adds) + (1+2+4+...+n) (copies)
 *                        ≤ n + 2n = 3n = O(n) total → O(1) amortized
 *
 * Space Complexity:
 *   Auxiliary:    O(1) per operation
 *   Total array:  O(n) — at most 2n capacity after n adds
 *   Wasted space: ≤ 50% (capacity is at most 2 × size)
 *
 * Recurrence: N/A (not recursive)
 *
 * Bottleneck: Resize operations — occur at sizes 1, 2, 4, 8, ..., n
 *             Only O(log n) resizes in n operations
 * Tight bound: Amortized Θ(1) per add confirmed by potential method:
 *              Φ(D) = 2·size - capacity; each add: âᵢ = 3 = O(1)
 * ═══════════════════════════════════════════
 */
```

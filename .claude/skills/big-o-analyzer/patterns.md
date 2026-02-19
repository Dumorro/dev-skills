# Algorithmic Patterns: Anti-Patterns vs. Optimized Solutions

## Pattern 1: Lookup in a Loop

### 🚨 Anti-Pattern — O(n²)
```typescript
function findDuplicates(arr: number[]): number[] {
  const duplicates: number[] = [];
  for (const item of arr) {
    // .includes() is O(n) inside an O(n) loop = O(n²)
    if (arr.indexOf(item) !== arr.lastIndexOf(item) &&
        !duplicates.includes(item)) {
      duplicates.push(item);
    }
  }
  return duplicates;
}
```

### ✅ Optimized — O(n)
```typescript
function findDuplicates(arr: number[]): number[] {
  const seen = new Set<number>();
  const duplicates = new Set<number>();
  for (const item of arr) {
    if (seen.has(item)) duplicates.add(item); // O(1)
    else seen.add(item);                       // O(1)
  }
  return [...duplicates];
}
// Time: O(n) | Space: O(n)
```

---

## Pattern 2: Frequency Count

### 🚨 Anti-Pattern — O(n²)
```typescript
function mostFrequent(arr: string[]): string {
  let max = 0, result = '';
  for (const item of arr) {
    const count = arr.filter(x => x === item).length; // O(n) inside O(n)
    if (count > max) { max = count; result = item; }
  }
  return result;
}
```

### ✅ Optimized — O(n)
```typescript
function mostFrequent(arr: string[]): string {
  const freq = new Map<string, number>();
  for (const item of arr) {
    freq.set(item, (freq.get(item) ?? 0) + 1); // O(1)
  }
  return [...freq.entries()].reduce((a, b) => b[1] > a[1] ? b : a)[0];
}
// Time: O(n) | Space: O(k) where k = unique elements
```

---

## Pattern 3: Two Sum / Pair Problems

### 🚨 Anti-Pattern — O(n²)
```typescript
function twoSum(nums: number[], target: number): [number, number] | null {
  for (let i = 0; i < nums.length; i++)
    for (let j = i + 1; j < nums.length; j++) // Nested loop
      if (nums[i] + nums[j] === target) return [i, j];
  return null;
}
```

### ✅ Optimized — O(n)
```typescript
function twoSum(nums: number[], target: number): [number, number] | null {
  const seen = new Map<number, number>(); // value → index
  for (let i = 0; i < nums.length; i++) {
    const complement = target - nums[i];
    if (seen.has(complement)) return [seen.get(complement)!, i]; // O(1)
    seen.set(nums[i], i);
  }
  return null;
}
// Time: O(n) | Space: O(n)
```

---

## Pattern 4: Sliding Window

### 🚨 Anti-Pattern — O(n²)
```typescript
// Max sum subarray of size k
function maxSubarraySum(arr: number[], k: number): number {
  let max = -Infinity;
  for (let i = 0; i <= arr.length - k; i++) {
    let sum = 0;
    for (let j = i; j < i + k; j++) sum += arr[j]; // Recomputes each time
    max = Math.max(max, sum);
  }
  return max;
}
```

### ✅ Optimized Sliding Window — O(n)
```typescript
function maxSubarraySum(arr: number[], k: number): number {
  let windowSum = arr.slice(0, k).reduce((a, b) => a + b, 0);
  let max = windowSum;
  for (let i = k; i < arr.length; i++) {
    windowSum += arr[i] - arr[i - k]; // Slide: add new, remove old
    max = Math.max(max, windowSum);
  }
  return max;
}
// Time: O(n) | Space: O(1)
```

---

## Pattern 5: Top-K Elements

### 🚨 Anti-Pattern — O(n log n)
```typescript
// Sort and take k — wasteful when k << n
function topK(nums: number[], k: number): number[] {
  return nums.sort((a, b) => b - a).slice(0, k);
}
```

### ✅ Optimized Min-Heap — O(n log k)
```typescript
// Use a min-heap of size k (pseudocode — use a heap library in production)
// For JS, a common trick with sorted insertion into bounded array:
function topK(nums: number[], k: number): number[] {
  const heap: number[] = [];
  for (const num of nums) {
    heap.push(num);
    heap.sort((a, b) => a - b); // Min at front
    if (heap.length > k) heap.shift(); // O(log k) with real heap
  }
  return heap.sort((a, b) => b - a);
}
// With proper min-heap: Time O(n log k) | Space O(k)
// Prefer k << n; otherwise sorting is acceptable
```

---

## Pattern 6: Memoization for Recursion

### 🚨 Anti-Pattern — O(2ⁿ)
```typescript
function fibonacci(n: number): number {
  if (n <= 1) return n;
  return fibonacci(n - 1) + fibonacci(n - 2); // Recomputes subproblems!
}
```

### ✅ Optimized Memoization — O(n)
```typescript
function fibonacci(n: number, memo = new Map<number, number>()): number {
  if (n <= 1) return n;
  if (memo.has(n)) return memo.get(n)!;
  const result = fibonacci(n - 1, memo) + fibonacci(n - 2, memo);
  memo.set(n, result);
  return result;
}
// Time: O(n) | Space: O(n)

// Or bottom-up DP with O(1) space:
function fibDP(n: number): number {
  if (n <= 1) return n;
  let [prev, curr] = [0, 1];
  for (let i = 2; i <= n; i++) [prev, curr] = [curr, prev + curr];
  return curr;
}
// Time: O(n) | Space: O(1)
```

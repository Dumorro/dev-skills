# Big O Notation Reference

## Complexity Hierarchy (Best → Worst)

| Notation     | Name         | Example                          |
|--------------|--------------|----------------------------------|
| O(1)         | Constant     | Hash map lookup, array index     |
| O(log n)     | Logarithmic  | Binary search, balanced BST      |
| O(n)         | Linear       | Single loop, linear scan         |
| O(n log n)   | Linearithmic | Merge sort, heap sort, Tim sort  |
| O(n²)        | Quadratic    | Nested loops, bubble sort        |
| O(n³)        | Cubic        | Triple nested loops              |
| O(2ⁿ)        | Exponential  | Recursive Fibonacci (naive)      |
| O(n!)        | Factorial    | Permutations, brute-force TSP    |

## Data Structure Complexities

| Structure        | Access | Search | Insert | Delete | Space |
|------------------|--------|--------|--------|--------|-------|
| Array            | O(1)   | O(n)   | O(n)   | O(n)   | O(n)  |
| Linked List      | O(n)   | O(n)   | O(1)   | O(1)   | O(n)  |
| Stack / Queue    | O(n)   | O(n)   | O(1)   | O(1)   | O(n)  |
| Hash Table       | —      | O(1)*  | O(1)*  | O(1)*  | O(n)  |
| Binary Search Tree | O(log n)* | O(log n)* | O(log n)* | O(log n)* | O(n) |
| AVL / Red-Black  | O(log n) | O(log n) | O(log n) | O(log n) | O(n) |
| Heap (Min/Max)   | O(1) top | O(n)  | O(log n) | O(log n) | O(n) |
| Trie             | O(m)   | O(m)   | O(m)   | O(m)   | O(n·m)|
| Graph (Adj. List)| —      | O(V+E) | O(1)   | O(E)   | O(V+E)|
| Graph (Adj. Matrix)| O(1) | O(V²)  | O(1)   | O(1)   | O(V²) |

*Average case. Worst case may be O(n) due to hash collisions.

## Sorting Algorithm Complexities

| Algorithm      | Best       | Average    | Worst      | Space    | Stable |
|----------------|------------|------------|------------|----------|--------|
| Bubble Sort    | O(n)       | O(n²)      | O(n²)      | O(1)     | Yes    |
| Selection Sort | O(n²)      | O(n²)      | O(n²)      | O(1)     | No     |
| Insertion Sort | O(n)       | O(n²)      | O(n²)      | O(1)     | Yes    |
| Merge Sort     | O(n log n) | O(n log n) | O(n log n) | O(n)     | Yes    |
| Quick Sort     | O(n log n) | O(n log n) | O(n²)      | O(log n) | No     |
| Heap Sort      | O(n log n) | O(n log n) | O(n log n) | O(1)     | No     |
| Tim Sort       | O(n)       | O(n log n) | O(n log n) | O(n)     | Yes    |
| Counting Sort  | O(n+k)     | O(n+k)     | O(n+k)     | O(k)     | Yes    |
| Radix Sort     | O(nk)      | O(nk)      | O(nk)      | O(n+k)   | Yes    |

## Algorithm Complexities by Category

### Search
| Algorithm        | Time        | Space   | Notes                       |
|------------------|-------------|---------|---------------------------- |
| Linear Search    | O(n)        | O(1)    | Unsorted data               |
| Binary Search    | O(log n)    | O(1)    | Requires sorted data        |
| BFS              | O(V+E)      | O(V)    | Shortest path (unweighted)  |
| DFS              | O(V+E)      | O(V)    | Cycle detection, topo sort  |

### Graph Shortest Path
| Algorithm        | Time              | Space  | Use Case                    |
|------------------|-------------------|--------|-----------------------------|
| Dijkstra         | O((V+E) log V)    | O(V)   | Non-negative weights        |
| Bellman-Ford     | O(V·E)            | O(V)   | Negative weights            |
| Floyd-Warshall   | O(V³)             | O(V²)  | All-pairs shortest path     |
| A*               | O(E)              | O(V)   | Heuristic-guided            |

### Dynamic Programming Indicators
Apply DP when:
- Problem has **overlapping subproblems**
- Problem has **optimal substructure**
- Naive recursion has exponential complexity

Common DP optimizations:
- Memoization (top-down): cache recursive results
- Tabulation (bottom-up): fill a table iteratively
- Space optimization: reduce O(n) DP table to O(1) when only previous row needed

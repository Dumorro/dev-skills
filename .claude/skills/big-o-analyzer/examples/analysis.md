# Real-World Complexity Analysis Examples

## Example 1: User Permission Check

```typescript
/**
 * Check if user has required permissions.
 *
 * Complexity Analysis:
 * Time:  O(p) where p = number of user permissions
 *        (Set.has is O(1), so overall O(p) for construction)
 * Space: O(p) for the permission Set
 *
 * Bottleneck: None significant for typical permission counts
 * Alternative: If permissions are static, pre-build the Set once per session
 *              to reduce to O(1) per check after initialization.
 */
function hasPermission(userPermissions: string[], required: string[]): boolean {
  const permSet = new Set(userPermissions); // O(p)
  return required.every(r => permSet.has(r)); // O(r) where r = required.length
}
// Total: O(p + r) — far better than O(p * r) with array.includes
```

---

## Example 2: Database Query N+1 Anti-Pattern (Backend)

```typescript
// 🚨 N+1 QUERY PROBLEM — O(n) database round trips
async function getUsersWithOrdersBad(userIds: string[]) {
  const users = await db.users.findMany({ where: { id: { in: userIds } } });
  for (const user of users) {
    user.orders = await db.orders.findMany({ where: { userId: user.id } });
    // ↑ This fires n separate queries!
  }
  return users;
}

// ✅ Single query with JOIN — O(1) round trips
async function getUsersWithOrdersGood(userIds: string[]) {
  return db.users.findMany({
    where: { id: { in: userIds } },
    include: { orders: true }, // Single JOIN query
  });
}
/**
 * Complexity Analysis:
 * Bad:  O(n) database round trips → latency compounds with n
 * Good: O(1) round trips → single optimized JOIN
 * Space: O(u + o) where u = users, o = total orders returned
 */
```

---

## Example 3: Graph BFS vs DFS Decision

```typescript
/**
 * Use BFS when: finding SHORTEST PATH (unweighted), level-order traversal.
 * Use DFS when: cycle detection, topological sort, connected components.
 *
 * Complexity Analysis (both):
 * Time:  O(V + E) — visits every vertex and edge once
 * Space: O(V) — queue (BFS) or call stack (DFS)
 */
function bfs(graph: Map<number, number[]>, start: number): number[] {
  const visited = new Set<number>();
  const queue: number[] = [start];
  const result: number[] = [];

  while (queue.length > 0) {
    const node = queue.shift()!; // Use a proper deque in production
    if (visited.has(node)) continue;
    visited.add(node);
    result.push(node);
    for (const neighbor of graph.get(node) ?? []) {
      if (!visited.has(neighbor)) queue.push(neighbor);
    }
  }
  return result;
}
// Note: Array.shift() is O(n) — use a linked-list queue for true O(1) dequeue
// With proper queue: Time O(V+E) | Space O(V)
```

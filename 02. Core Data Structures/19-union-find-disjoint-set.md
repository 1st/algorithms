# 19 · Union-Find (Disjoint Set Union)

Union-Find (Disjoint Set Union, DSU) efficiently tracks connected components in a dynamic graph. It supports near-constant-time union and find operations, powering Kruskal’s MST algorithm and connectivity queries.

## Learning objectives
- Understand the union-by-rank/size and path compression optimizations
- Implement Union-Find in Python with amortised `α(n)` complexity
- Apply DSU to connectivity, cycle detection, and grouping problems
- Recognise when DSU outperforms DFS/BFS for incremental connectivity

## Core operations
- `find(x)`: return representative (root) of the set containing `x`.
- `union(x, y)`: merge the sets containing `x` and `y`.
- `connected(x, y)`: check if `find(x) == find(y)`.

## Python implementation

```python
class UnionFind:
    def __init__(self, elements: list[int]):
        self.parent = {x: x for x in elements}
        self.rank = {x: 0 for x in elements}  # or size

    def find(self, x: int) -> int:
        if self.parent[x] != x:
            self.parent[x] = self.find(self.parent[x])  # path compression
        return self.parent[x]

    def union(self, x: int, y: int) -> bool:
        root_x = self.find(x)
        root_y = self.find(y)
        if root_x == root_y:
            return False
        if self.rank[root_x] < self.rank[root_y]:
            self.parent[root_x] = root_y
        elif self.rank[root_x] > self.rank[root_y]:
            self.parent[root_y] = root_x
        else:
            self.parent[root_y] = root_x
            self.rank[root_x] += 1
        return True
```

- **Path compression** flattens the tree on `find`.
- **Union by rank/size** attaches smaller tree under larger root.
- Amortised complexity: `O(α(n))`, inverse Ackermann—effectively constant.

## Use cases
- Dynamic connectivity: determine if two nodes are in the same component.
- Detect cycles while adding edges (if `union` returns `False`, edge closes a cycle).
- Kruskal’s MST algorithm: sort edges, union endpoints, skip if already connected.
- Grouping problems (e.g., accounts merge, friend circles).

## Interview checkpoints
- Explain why naive union-find degenerates and how optimizations fix it.
- Mention the near-constant amortised complexity (`α(n)`).
- Show how to adapt DSU for additional metadata (component size, value aggregation).

## Further practice
- Implement Kruskal’s algorithm using DSU.
- Solve “number of islands II” (dynamic island counting) with union-find.
- Extend DSU to support rollback operations (used in offline queries).

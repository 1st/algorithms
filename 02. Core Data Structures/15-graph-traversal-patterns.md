# 15 · Graph Traversal Patterns

Traversal algorithms reveal structure, connectivity, and shortest paths in graphs. Depth-first search (DFS) and breadth-first search (BFS) form the foundation for many interview problems.

## Learning objectives
- Implement DFS and BFS in Python using adjacency lists
- Understand time and space complexity relative to `|V|` and `|E|`
- Apply traversal patterns to cycle detection, connected components, and topological sorting
- Manage visited sets to avoid infinite loops in cyclic graphs

## Depth-first search (DFS)

```python
from collections import defaultdict
from typing import Dict, List, Set

Graph = Dict[str, List[str]]

def dfs(graph: Graph, start: str) -> list[str]:
    visited: Set[str] = set()
    order: list[str] = []

    def visit(node: str) -> None:
        visited.add(node)
        order.append(node)
        for neighbor in graph[node]:
            if neighbor not in visited:
                visit(neighbor)

    visit(start)
    return order
```

- Time: `O(|V| + |E|)`.
- Space: `O(|V|)` recursion stack (or explicit stack for iterative version).
- Variants: iterative DFS (stack), multi-source DFS, postorder for topological sort.

### Use cases
- Detect cycles (track recursion stack).
- Enumerate connected components (run DFS from unvisited nodes).
- Solve pathfinding in mazes with backtracking.

## Breadth-first search (BFS)

```python
from collections import deque

def bfs(graph: Graph, start: str) -> list[str]:
    visited: set[str] = {start}
    order: list[str] = []
    queue: deque[str] = deque([start])
    while queue:
        node = queue.popleft()
        order.append(node)
        for neighbor in graph[node]:
            if neighbor not in visited:
                visited.add(neighbor)
                queue.append(neighbor)
    return order
```

- Time: `O(|V| + |E|)`.
- Space: up to `O(|V|)` for queue and visited set.
- Shortest path in unweighted graphs: track parent pointers to reconstruct routes.

### Use cases
- Shortest path (unweighted) between two nodes.
- Level-order traversal (graph or tree).
- Checking bipartiteness by coloring levels.

## Topological sort (DAGs)
Combine DFS or BFS (Kahn’s algorithm) to order tasks with dependencies.

```python
def topological_sort(graph: Graph) -> list[str]:
    indegree: dict[str, int] = {node: 0 for node in graph}
    for neighbors in graph.values():
        for v in neighbors:
            indegree[v] = indegree.get(v, 0) + 1
    queue = deque(node for node, deg in indegree.items() if deg == 0)
    order: list[str] = []
    while queue:
        node = queue.popleft()
        order.append(node)
        for neighbor in graph.get(node, []):
            indegree[neighbor] -= 1
            if indegree[neighbor] == 0:
                queue.append(neighbor)
    if len(order) != len(indegree):
        raise ValueError("Graph has a cycle")
    return order
```

## Managing visited state
- Use `set` for visited nodes.
- For weighted graphs, track visited separately from distance map to avoid stale entries.
- In directed graphs, maintain recursion stack for cycle detection.

## Interview checkpoints
- Outline time/space complexity before coding (`O(|V| + |E|)`).
- Recognise when to switch from recursion to explicit stacks/queues to avoid recursion limits.
- Specify behavior for disconnected graphs (loop through all nodes).

## Further practice
- Implement cycle detection (directed vs. undirected) using traversal variants.
- Solve “shortest path in binary matrix” and “number of islands” problems.
- Apply BFS to state-space search (e.g., word ladder).

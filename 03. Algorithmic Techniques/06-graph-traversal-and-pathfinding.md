# 06 · Graph Traversal and Pathfinding

Graph algorithms generalise traversals from trees to arbitrary networks. Mastering BFS, DFS, and shortest-path techniques enables solutions to connectivity, routing, and dependency problems.

## Learning objectives
- Choose appropriate traversal (BFS, DFS) for unweighted graphs and understand their complexity
- Implement shortest-path algorithms (Dijkstra, Bellman-Ford, A*) based on graph properties
- Detect cycles, compute connected components, and handle directed acyclic graphs (DAGs)
- Combine traversal with state-tracking for puzzles and pathfinding problems

## Traversal recap
- **BFS:** explores by layers; shortest path in unweighted graphs.
- **DFS:** explores deeply; useful for cycle detection, topological sort, and component enumeration.
- Time complexity for adjacency lists: `O(|V| + |E|)`.

```python
from collections import deque

def shortest_path_unweighted(graph, source, target):
    queue = deque([source])
    parent = {source: None}
    while queue:
        node = queue.popleft()
        if node == target:
            break
        for neighbor in graph[node]:
            if neighbor not in parent:
                parent[neighbor] = node
                queue.append(neighbor)
    if target not in parent:
        return []
    path = []
    node = target
    while node is not None:
        path.append(node)
        node = parent[node]
    return list(reversed(path))
```

## Single-source shortest paths
- **Dijkstra:** non-negative weights (`O((|V| + |E|) log |V|)` with heap).
- **Bellman-Ford:** handles negative weights, detects negative cycles (`O(|V||E|)`).
- **Topological DP:** for DAGs with weighted edges; process nodes in topological order, relax edges once (`O(|V| + |E|)`).

```python
def dag_shortest_path(graph, topo_order, source):
    dist = {node: float("inf") for node in topo_order}
    dist[source] = 0
    for node in topo_order:
        if dist[node] == float("inf"):
            continue
        for neighbor, weight in graph[node]:
            if dist[node] + weight < dist[neighbor]:
                dist[neighbor] = dist[node] + weight
    return dist
```

## All-pairs shortest paths
- **Floyd-Warshall:** `O(|V|^3)` dynamic programming for dense graphs.
- **Repeated Dijkstra:** run Dijkstra from each node (`O(|V||E| log |V|)`).

## Heuristic search (A*)
- Combines Dijkstra with heuristic `h(n)` estimating distance to goal.
- Must be admissible (never overestimates) for optimality.
- Common in grid-based pathfinding; heuristics include Manhattan and Euclidean distance.

## Additional patterns
- **Connectivity:** use DSU for dynamic connectivity or BFS/DFS for static checks.
- **Bridges & articulation points:** DFS with discovery/low times (Tarjan’s algorithm).
- **Topological sort:** detect cycles in DAGs; prerequisites scheduling.
- **Minimum spanning tree:** Prim’s (greedy with heap), Kruskal’s (edges sorted + DSU).

## Interview checkpoints
- Clarify graph traits (directed/undirected, weighted/unweighted, negative edges) before selecting algorithm.
- State complexity in terms of `|V|` and `|E|`.
- Highlight visited tracking to avoid infinite loops; mention resetting for multiple components.
- For path reconstruction, show parent pointer tracking or store predecessor info.

## Further practice
- Solve shortest path in binary matrix, word ladder, and network delay time.
- Implement Tarjan’s bridge and articulation-point algorithms.
- Explore A* with heuristics on grid mazes for game-like problems.

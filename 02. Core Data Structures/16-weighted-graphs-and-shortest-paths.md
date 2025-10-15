# 16 · Weighted Graphs and Shortest Paths

Weighted graphs assign costs to edges. Shortest-path algorithms like Dijkstra, Bellman-Ford, and Floyd-Warshall compute minimum-cost routes—essential for network routing, navigation, and many interview problems.

## Learning objectives
- Represent weighted graphs effectively for algorithm use
- Implement Dijkstra’s algorithm with a priority queue in Python
- Understand when Bellman-Ford and Floyd-Warshall apply and their complexities
- Recognise negative cycles and adapt algorithms accordingly

## Weighted graph representation

```python
from collections import defaultdict
from typing import Dict, List, Tuple

WeightedGraph = Dict[str, List[Tuple[str, int]]]

def add_edge(graph: WeightedGraph, u: str, v: str, weight: int, directed: bool = False) -> None:
    graph[u].append((v, weight))
    if not directed:
        graph[v].append((u, weight))
```

Use adjacency lists with `(neighbor, weight)` pairs; adjacency matrices work for dense graphs but consume `O(|V|^2)` memory.

## Dijkstra’s algorithm (non-negative weights)

```python
import heapq

def dijkstra(graph: WeightedGraph, source: str) -> dict[str, float]:
    distances: dict[str, float] = {node: float("inf") for node in graph}
    distances[source] = 0.0
    heap: list[tuple[float, str]] = [(0.0, source)]
    while heap:
        dist, node = heapq.heappop(heap)
        if dist > distances[node]:
            continue  # stale entry
        for neighbor, weight in graph[node]:
            new_dist = dist + weight
            if new_dist < distances.get(neighbor, float("inf")):
                distances[neighbor] = new_dist
                heapq.heappush(heap, (new_dist, neighbor))
    return distances
```

- Complexity: `O((|V| + |E|) log |V|)` with a binary heap.
- Requires non-negative weights; negative edges break the greedy assumption.
- To reconstruct paths, store parent pointers while updating distances.

## Bellman-Ford (handles negative weights)
- Relax edges repeatedly (`|V| - 1` times); detect negative cycles on the `|V|`-th iteration.
- Complexity: `O(|V||E|)`.
- Use when graph contains negative weights but no negative cycles, or when you must detect such cycles.

## Floyd-Warshall (all-pairs shortest paths)
- Dynamic programming across all vertex pairs.
- Complexity: `O(|V|^3)`; suitable for dense graphs with up to a few hundred nodes.
- Works with negative edges (no negative cycles) and outputs distance matrix.

## Detecting negative cycles
- Bellman-Ford: after `|V| - 1` relaxations, iterate once more—if any distance improves, a negative cycle exists.
- Floyd-Warshall: if `dist[i][i] < 0` after completion, negative cycle reachable from `i`.

## When to choose each algorithm
- `Dijkstra`: non-negative weights, single-source shortest paths.
- `Bellman-Ford`: graphs with negative weights, single-source, cycle detection.
- `Floyd-Warshall`: dense graphs, all-pairs queries, moderate node counts.
- `A*`: heuristic-driven pathfinding (e.g., grids) when admissible heuristics available.

## Interview checkpoints
- State algorithm prerequisites (non-negative weights for Dijkstra).
- Discuss priority queue implementation details and complexity.
- Explain how to detect negative cycles and respond accordingly.

## Further practice
- Implement Bellman-Ford and detect negative cycles with sample graphs.
- Solve weighted shortest path problems (network delay time, cheapest flight with stops).
- Compare runtime on sparse vs. dense graphs to internalise complexity trade-offs.

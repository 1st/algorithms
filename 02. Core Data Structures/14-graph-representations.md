# 14 · Graph Representations

Graphs model relationships between entities. Choosing the right representation—adjacency list, adjacency matrix, or edge list—affects algorithm complexity and memory usage.

## Learning objectives
- Compare adjacency lists, matrices, and edge lists, including trade-offs
- Implement graph structures in Python using dictionaries and lists
- Identify when to use directed vs. undirected representations, weighted edges, and sparse vs. dense formats
- Prepare graphs for traversal algorithms discussed in later chapters

## Terminology
- **Vertices (nodes):** entities in the graph.
- **Edges:** connections between vertices (directed or undirected, weighted or unweighted).
- **Degree:** number of edges incident to a vertex (in-degree/out-degree for directed).
- **Sparse vs. dense:** sparse graphs have `|E| ≈ |V|`, dense graphs approach `|V|^2` edges.

## Representation comparison

| Representation | Storage | Best for | Pros | Cons |
| --- | --- | --- | --- | --- |
| Adjacency list | `O(|V| + |E|)` | Sparse graphs | Efficient traversal, dynamic | Lookup edge existence `O(deg)` |
| Adjacency matrix | `O(|V|^2)` | Dense graphs, matrix algos | Fast edge lookup `O(1)`, easy transposition | Memory-heavy, poor for sparse graphs |
| Edge list | `O(|E|)` | Graph algorithms needing edge streams | Simple to store, compact | Slow adjacency queries |

## Python patterns

```python
from collections import defaultdict

Graph = dict[str, list[tuple[str, int]]]

def add_edge(graph: Graph, u: str, v: str, weight: int = 1, directed: bool = False) -> None:
    graph[u].append((v, weight))
    if not directed:
        graph[v].append((u, weight))


graph: Graph = defaultdict(list)
add_edge(graph, "A", "B", 5)
add_edge(graph, "A", "C", 2, directed=True)
```

- Use `defaultdict(list)` for adjacency lists, storing `(neighbor, weight)` pairs.
- For matrices, use `list[list[int]]` or NumPy arrays when matrix operations matter.
- Edge lists can be stored as `list[tuple[u, v, weight]]`.

## Weighted vs. unweighted
- Weighted edges carry costs/lengths; BFS works directly on unweighted graphs but Dijkstra/Bellman-Ford handle weights.
- When weights are uniform, treat graph as unweighted to simplify algorithms.

## Directed vs. undirected
- Represent directed edges by storing separate adjacency entries (no symmetric addition).
- Track in-degree/out-degree for directed graphs when algorithms need them (topological sort).

## When to choose each representation
- **Adjacency list:** sparse graphs, general-purpose traversal, dynamic graph updates.
- **Adjacency matrix:** dense graphs, frequent `O(1)` edge lookups, algorithms relying on matrix multiplication (e.g., transitive closure).
- **Edge list:** MST algorithms (Kruskal), streaming edges from files/databases.

## Interview checkpoints
- State complexity impacts: adjacency matrix uses `O(|V|^2)` space—mention when `|V|` is large.
- Justify representation choice given problem constraints (sparse/dense, dynamic/static).
- Explain how to convert between representations if needed.

## Further practice
- Build converters between adjacency lists and matrices.
- Implement simple graph loaders from text files to internal representations.
- Experiment with large sparse vs. dense graphs to observe memory usage differences.

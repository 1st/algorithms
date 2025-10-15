# 04 · Greedy Strategies

Greedy algorithms build solutions step by step, making locally optimal choices that add up to a global optimum under specific conditions. They are efficient when the greedy choice property and optimal substructure hold.

## Learning objectives
- Identify problems where greedy strategies apply (and where they fail)
- Prove or justify greedy correctness using exchange arguments or matroid theory intuition
- Implement classic greedy algorithms (interval scheduling, Huffman coding, Prim’s algorithm)
- Combine greedy selection with sorting or priority queues in Python

## Greedy template
1. Define a scoring or ordering heuristic.
2. Sort or prioritise elements accordingly.
3. Iterate, accepting/rejecting choices based on feasibility.

## Classic examples

### Interval scheduling (max non-overlapping intervals)

```python
def select_intervals(intervals: list[tuple[int, int]]) -> list[tuple[int, int]]:
    intervals.sort(key=lambda x: x[1])  # earliest finish time
    result: list[tuple[int, int]] = []
    current_end = float("-inf")
    for start, finish in intervals:
        if start >= current_end:
            result.append((start, finish))
            current_end = finish
    return result
```

- Sorting by finish times ensures maximum compatible set (exchange argument).

### Huffman coding
- Build optimal prefix code by repeatedly merging two least frequent symbols using a min-heap.

### Kruskal’s algorithm (MST)
- Sort edges by weight, add if they connect different components (using DSU).

## Correctness techniques
- **Greedy choice property:** you can pick a globally optimal solution by making the best local choice.
- **Exchange argument:** assume optimal solution differs; swap selections to show greedy remains optimal without loss.
- **Matroids:** sets satisfying hereditary + exchange properties guarantee greedy optimality.

## When greedy fails
- Knapsack 0/1: greedy by value density fails; DP required.
- Scheduling with penalties or complex constraints.
- Situations lacking optimal substructure or with long-range dependencies.

## Data structures for greedy
- Sorting: `O(n log n)` preprocessing (interval scheduling, activity selection).
- Heaps/priority queues: dynamic selection (Huffman, Dijkstra, Prim).
- DSU: maintain components when merging edges (Kruskal).

## Interview checkpoints
- State why greedy works (greedy choice property) or acknowledge need for proof.
- Use counterexamples when interviewer tests understanding of greedy limitations.
- Combine greedy with other techniques (sorting + greedy, heap + union-find).

## Further practice
- Solve coin change (canonical coin systems) and provide counterexamples for non-canonical coins.
- Implement Prim’s algorithm for MST and compare with Kruskal.
- Work through scheduling problems with different objective functions.

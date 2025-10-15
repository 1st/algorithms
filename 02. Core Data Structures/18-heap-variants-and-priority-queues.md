# 18 · Heap Variants and Priority Queues

Beyond binary heaps, specialised heap variants optimise specific operations such as decrease-key or melding. Understanding their trade-offs prepares you for advanced interview questions and theoretical discussions.

## Learning objectives
- Compare binary, binomial, Fibonacci, and pairing heaps
- Recognise when decrease-key, meld, or amortised guarantees matter
- Build priority queues that suit real-world workloads using Python primitives

## Priority queue recap
Priority queues expose `push`, `pop`, and `peek` tied to priority ordering. Binary heaps power most practical implementations, but variants exist:

| Heap type | `insert` | `delete-min` | `decrease-key` | Meld | Notes |
| --- | --- | --- | --- | --- | --- |
| Binary heap | `O(log n)` | `O(log n)` | `O(log n)` (no native op in `heapq`) | `O(n)` | Simple, cache-friendly |
| Binomial heap | `O(log n)` | `O(log n)` | `O(log n)` | `O(log n)` | Supports meld efficiently |
| Fibonacci heap | `O(1)` amortised | `O(log n)` | `O(1)` amortised | `O(1)` | Theoretical best for Dijkstra with many decrease-key ops |
| Pairing heap | `O(1)` amortised | `O(log n)` amortised | `O(log n)` amortised | `O(1)` amortised | Practical alternative to Fibonacci |

### Binomial heap
- Forest of binomial trees (order `k` tree has `2^k` nodes).
- Merge combines root lists and carries over like binary addition.
- Delete-min removes smallest root and merges its subtrees back.

### Fibonacci heap
- Lazy merging of trees; decrease-key cuts subtrees and adds them to root list.
- Amortised bounds rely on potential method; heavy implementation overhead.
- Rare in production but discussed in theoretical contexts (e.g., CLRS).

### Pairing heap
- Self-adjusting heap with simple decrease-key implementation (cut and meld new subtree).
- Performs well in practice; simpler than Fibonacci heaps.

## Python priority queue patterns
- `heapq` for typical applications; wrap elements as `(priority, counter, value)` to avoid comparisons of equal priorities.
- `queue.PriorityQueue` adds thread safety but with higher overhead.
- Third-party libraries (`heapdict`) offer decrease-key support.

```python
import heapq
from itertools import count

class PriorityQueue:
    def __init__(self):
        self._heap: list[tuple[int, int, object]] = []
        self._entry_finder: dict[object, tuple[int, int, object]] = {}
        self._counter = count()

    def push(self, item: object, priority: int) -> None:
        entry = (priority, next(self._counter), item)
        self._entry_finder[item] = entry
        heapq.heappush(self._heap, entry)

    def pop(self) -> object:
        priority, _, item = heapq.heappop(self._heap)
        while item not in self._entry_finder or self._entry_finder[item][0] != priority:
            priority, _, item = heapq.heappop(self._heap)
        del self._entry_finder[item]
        return item

    def decrease_key(self, item: object, new_priority: int) -> None:
        self._entry_finder.pop(item, None)
        entry = (new_priority, next(self._counter), item)
        self._entry_finder[item] = entry
        heapq.heappush(self._heap, entry)
```

This implementation performs lazy deletion: outdated entries remain in the heap until popped.

## When to prefer heap variants
- **Binomial heap:** efficient meld operations (union of two queues).
- **Fibonacci/pairing heap:** heavy use of decrease-key (graph algorithms with many edge relaxations).
- **Binary heap:** general-purpose; best constants for most workloads.

## Interview checkpoints
- Compare heap variants succinctly; mention real-world usage vs. theoretical optimums.
- Explain lazy deletion for decrease-key in languages without native support.
- Tie variants to algorithms (e.g., Dijkstra with Fibonacci heap achieves `O(|E| + |V| log |V|)`).

## Further practice
- Implement a binomial heap merge by hand to understand its structure.
- Benchmark binary vs. pairing heap (using external libraries) on workloads with many decrease-key operations.
- Research how languages like C++ (`std::priority_queue`) or Java implement priority queues.

# 22 · LRU Caches

Least Recently Used (LRU) caches evict the item that has gone unused for the longest time. Implementations typically combine hash maps with doubly linked lists to achieve `O(1)` get/put operations.

## Learning objectives
- Describe how LRU caches track usage order with linked lists or deques
- Implement an `O(1)` LRU cache in Python using `OrderedDict` or custom nodes
- Evaluate memory/time trade-offs and compare with LFU/FIFO alternatives
- Recognise interview scenarios that require cache invalidation logic

## Core structure
- Hash map maps keys → nodes for constant-time lookup.
- Doubly linked list stores nodes in usage order; head = most recent, tail = least recent.
- On `get(key)`, move node to head. On `put`, insert/update node at head and evict tail if over capacity.

## Python implementation

```python
from collections import OrderedDict

class LRUCache:
    def __init__(self, capacity: int):
        self.capacity = capacity
        self.store: OrderedDict[int, int] = OrderedDict()

    def get(self, key: int) -> int:
        if key not in self.store:
            return -1
        value = self.store.pop(key)
        self.store[key] = value  # reinsert to move to end
        return value

    def put(self, key: int, value: int) -> None:
        if key in self.store:
            self.store.pop(key)
        elif len(self.store) >= self.capacity:
            self.store.popitem(last=False)  # evict least-recently used
        self.store[key] = value
```

- `OrderedDict` (Py ≥3.7) preserves insertion order; moving items to end updates recency.
- For interview implementations without `OrderedDict`, use custom doubly linked list nodes plus dictionary referencing nodes.

## Complexity
- `get`, `put`: `O(1)` average time.
- Space: `O(capacity)`.

## Variants
- **LFU cache:** evict least frequently used; requires frequency tracking.
- **MRU cache:** evict most recently used (certain workloads).
- **Segmented LRU:** split cache into segments (probation/protected) to handle scan resistance.
- **Time-to-live (TTL):** store expiration timestamps; periodically purge stale entries.

## When to use LRU
- Limited memory caches with strong recency correlation (web caches, DB page caches).
- Interview problems requiring data structure with `O(1)` updates and eviction policy.
- Combined with Bloom filters to avoid caching negative lookups.

## Interview checkpoints
- Explain why naive list plus dictionary fails (`O(n)` removal). Highlight the need for doubly linked list.
- Mention edge cases: capacity 0, repeated puts, concurrency concerns if multi-threaded.
- Show how to adapt for thread safety (locks) or TTLs.

## Further practice
- Implement custom linked-list-based LRU without `OrderedDict`.
- Extend to LFU or ARC caches to compare eviction strategies.
- Integrate LRU cache into memoization problems (e.g., caching expensive API calls).

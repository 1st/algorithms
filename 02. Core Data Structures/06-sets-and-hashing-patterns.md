# 06 · Sets and Hashing Patterns

Sets are hash tables without values—only unique keys. They power membership tests, duplicate elimination, and many canonical interview idioms.

## Learning objectives
- Use Python’s `set` and `frozenset` effectively for constant-time membership
- Apply hashing patterns (dedupe, sliding window, frequency tracking) to common problems
- Understand how collision resolution and load factors influence set performance
- Recognise when to choose immutable vs. mutable sets

## Operations quick reference

| Operation | Python `set` | Average complexity | Notes |
| --- | --- | --- | --- |
| Membership test | `x in s` | `O(1)` | Hash then probe bucket |
| Insert | `s.add(x)` | `O(1)` amortised | Resizes as needed |
| Remove | `s.remove(x)` / `discard` | `O(1)` amortised | `discard` avoids KeyError |
| Iteration | `for x in s` | `O(n)` | Preserves insertion order (CPython 3.7+) |
| Set algebra | `s1 | s2`, `s1 & s2`, etc. | `O(len(s1) + len(s2))` | Loops through smaller set first |

## Python specifics
- `set` uses the same hash-table engine as `dict` (keys only). Order preservation mirrors dictionaries.
- `frozenset` is immutable and hashable—ideal for keys in other dictionaries/sets.
- Avoid mutating the underlying values that influence their hash; store immutable representations (`tuple`, `frozenset`) when necessary.

### Common patterns

```python
def has_duplicate(nums: list[int]) -> bool:
    seen: set[int] = set()
    for num in nums:
        if num in seen:
            return True
        seen.add(num)
    return False
```

- **Sliding window with uniqueness constraint:** maintain a window `set`, move left pointer when duplicates appear (e.g., longest substring without repeating characters).
- **Two-sum using membership:** store complements in a set to check in `O(n)`.
- **Top-K frequency problems:** combine `Counter` (dict-based) with sets for dedupe.

## Collision strategies recap
Sets share collision behaviour with dictionaries—open addressing in CPython. Understanding probe sequences helps when performance degrades:
- Heavy clustering increases lookup steps; rehash or increase table size.
- Poor hash functions (e.g., sequential integers modulo small base) can cause repeated collisions—random perturbation inside CPython mitigates this, but stay aware when designing custom hashes.

## When to choose sets
- Need fast membership tests without caring about ordering.
- Removing duplicates from large datasets.
- Tracking visited states in graph/DFS/BFS problems.

## When to look elsewhere
- Require ordering → use `list` + `bisect`, `heapq`, or `sortedcontainers` (third-party).
- Need counting → `collections.Counter` or dictionaries.
- Large, sparse universes with strict memory limits → Bitsets or Bloom filters (see next chapter).

## Interview checkpoints
- Justify `O(1)` average membership while acknowledging worst-case `O(n)` due to collisions.
- Call out the difference between `remove` and `discard`.
- Explain how to implement set union or intersection manually if language lacks built-ins.

## Further practice
- Solve “longest substring without repeating characters” and “contains duplicate” variations.
- Combine sets with BFS to track visited nodes efficiently.
- Benchmark `set` vs. list membership to internalise constant vs. linear lookup.

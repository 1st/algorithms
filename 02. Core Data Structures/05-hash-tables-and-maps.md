# 05 · Hash Tables and Maps

Hash tables map keys to values in near-constant time by computing an index from the key. Interviews love them because they offer simple APIs with subtle performance considerations.

## Learning objectives
- Understand how hashing, buckets, and collision resolution interact
- Recall average vs. worst-case complexities for lookup, insert, delete
- Use Python’s `dict` effectively, including iteration order and memory considerations
- Recognise when load factors and resizing impact performance

## Operations quick reference

| Operation | Python `dict` | Average complexity | Worst case |
| --- | --- | --- | --- |
| Lookup by key | `table[key]` | `O(1)` | `O(n)` if all keys collide |
| Insert / update | `table[key] = value` | `O(1)` amortised | `O(n)` |
| Delete | `del table[key]` | `O(1)` amortised | `O(n)` |
| Iteration | `for key in table` | `O(n)` | `O(n)` |

Python uses open addressing with perturbation to spread probes across buckets. Resizing happens automatically when the load factor crosses a threshold (~2/3 full).

## Anatomy of a hash table
1. **Hash function:** transforms a key into an integer (hash code).
2. **Compression:** maps the hash code into a table index (`hash % capacity` or similar).
3. **Buckets:** store entries; strategy varies (chains vs. open addressing).
4. **Collision resolution:** decides what to do when two keys map to the same index.

### Open addressing vs. separate chaining
- **Open addressing:** store one entry per bucket; collisions probe subsequent slots (linear, quadratic, double hashing). Keeps memory compact, but clustering hurts performance.
- **Separate chaining:** each bucket references a linked list or dynamic array of entries. Simplifies deletions and supports high load factors but adds pointer overhead.

## Python specifics
- `dict` preserves insertion order (CPython 3.7+) thanks to a compact array of indices plus separate key/value storage.
- Hashing custom objects: implement `__hash__` and `__eq__` consistently; ensure hashes remain stable for the object’s lifetime.
- Avoid mutating keys: if you change a field influencing `__hash__`, lookups break.

```python
def group_anagrams(words: list[str]) -> dict[tuple[int, ...], list[str]]:
    result: dict[tuple[int, ...], list[str]] = {}
    for word in words:
        signature = [0] * 26
        for ch in word:
            signature[ord(ch) - ord("a")] += 1
        key = tuple(signature)
        result.setdefault(key, []).append(word)
    return result
```

Using tuples (immutable, hashable) as keys allows grouping by signature efficiently.

## Load factor and resizing
- Load factor (`λ = entries / buckets`) influences probe length. Keep it below ~0.75 for open addressing.
- Resizing copies all entries into a larger table (`O(n)`), but occurs rarely enough to keep amortised costs near constant.
- `dict` grows by powers of two; newly allocated tables leave empty slots (sparse to reduce collisions).

## When to choose hash tables
- Need constant-time lookups and inserts without maintaining order.
- Keys map to unique values (dictionaries) or membership checks (sets, covered separately).
- Many interview problems reduce to counting occurrences or caching results—hash tables shine here.

> **Interview tip:** Say “average-case `O(1)` because load factor stays below ~0.75; worst-case `O(n)` if all keys collide.” Acknowledging both cases shows balanced understanding.

## When to look elsewhere
- Require sorted iteration → use balanced trees or heaps.
- Need range queries → consider ordered maps or segment trees.
- Keys must support full-text search or prefix matching → tries.

> **Common pitfall:** Mutating an object used as a dictionary key; remind the interviewer that hash and equality must remain stable or lookups break.

## Interview checkpoints
- Explain how collisions are handled and the impact on complexity.
- Mention that worst-case operations degrade to `O(n)` but are rare with good hash functions and low load factor.
- Discuss memory overhead: each entry stores key, value, hash, and metadata.

## Further practice
- Implement a simple hash map with separate chaining to solidify the mechanics.
- Analyse how `collections.Counter` and `defaultdict` extend hash tables.
- Tackle problems like two-sum, anagram grouping, and LRU caches to reinforce usage.

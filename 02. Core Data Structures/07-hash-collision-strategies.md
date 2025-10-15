# 07 · Hash Collision Strategies

Collisions are inevitable—different keys can generate the same hash bucket. Robust hash tables choose strategies that keep average performance near `O(1)` even when buckets fill.

## Learning objectives
- Compare common collision-resolution techniques and their trade-offs
- Understand how load factor and probing strategy interact
- Recognise scenarios where rehashing or alternative structures outperform naive approaches

## Core strategies

### Separate chaining
- Store a collection (linked list, dynamic array) per bucket.
- **Pros:** simple to implement, supports high load factors (>1), deletion is straightforward.
- **Cons:** extra memory per node, cache misses when traversing chains.
- **Optimisations:** use small dynamic arrays for short chains; switch to binary trees for long chains (Java 8+).

### Open addressing
Store at most one entry per bucket; collisions probe alternative slots.

| Strategy | Probe sequence | Notes |
| --- | --- | --- |
| Linear probing | `i, i+1, i+2, …` | Simple, but clustering can occur; benefits from table sizes that are powers of two and uniform hash codes. |
| Quadratic probing | `i, i+1², i+2², …` | Reduces clustering; ensure table size is prime or probing covers all buckets. |
| Double hashing | `i, i + f(key), i + 2f(key), …` | Uses a second hash to jump—spreads probes evenly but requires good secondary function. |

- **Deletion:** mark deleted slots with tombstones to avoid breaking probe chains.
- **Load factor:** keep below ~0.7; high load factor dramatically increases probe length.

### Cuckoo hashing
- Two (or more) hash functions; each key can reside in one of the candidate buckets.
- On collision, kick out the existing key and relocate it using its alternate hash—a “cuckoo” eviction.
- Guarantees `O(1)` lookup; needs occasional rehashes when cycles occur.

### Robin Hood hashing
- Variant of open addressing: when collisions occur, prefer the key with the longer probe distance, “stealing” a better slot for the disadvantaged entry.
- Balances probe lengths, improving worst-case behaviour.

## Load factor management
- **Resizing:** when load factor exceeds threshold, allocate a larger table and reinsert all entries (`O(n)`).
- **Rehashing:** sometimes triggered when too many collisions accumulate, even if table size stays constant.
- Monitor load factor as `entries / buckets`; design API to expose resizing behaviour if necessary (e.g., Java’s `HashMap`).

## Choosing a strategy
- **High write frequency + simple implementation:** separate chaining.
- **Memory-tight environments:** open addressing avoids pointer overhead.
- **Real-time lookups demanding low variance:** robin hood or cuckoo hashing reduce probe length swings.
- **Cache-conscious designs:** linear probing benefits from localized memory access.

## Interview checkpoints
- Explain why poor hash functions or high load factors degrade performance to `O(n)`.
- Describe how tombstones work in open addressing to support deletion.
- Discuss trade-offs when confronted with interviewer prompts like “design a hash map for millions of keys.”

## Further practice
- Implement a hash map twice: once with separate chaining, once with open addressing + linear probing.
- Experiment with load factors to observe performance degradation.
- Read CPython’s dictionary implementation notes for real-world engineering trade-offs.

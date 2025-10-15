# 01 · Data Structures Overview

Data structures are the containers that give your algorithms teeth. They organise data so that the operations you care about—lookup, insert, delete, iterate—are cheap.

## Learning objectives
- Map everyday engineering tasks to the data structure that fits best
- Understand the trade-offs between contiguous storage and pointer-based storage
- Recognise which Python primitives embody classic interview data structures

## Why data structures matter
- **Performance:** picking the wrong container quietly multiplies the cost of your algorithm.
- **Clarity:** the right abstraction makes the intent obvious to readers and interviewers.
- **Extensibility:** data structures often hint at additional features (ordering, caching, concurrency).

## Core families
- **Sequential containers:** arrays/lists, dynamic arrays, linked lists. Optimised for ordered traversal.
- **Hierarchical containers:** trees and heaps. Enable prioritisation, range queries, sorted iteration.
- **Associative containers:** hash tables, ordered maps/sets. Provide near-constant lookups keyed by value.
- **Graph representations:** adjacency lists and matrices. Capture relationships between entities.

Each family sacrifices something—memory, constant factors, ordering guarantees—to excel at specific operations.

## Python quick reference
- `list` → dynamic array; `append` is amortised `O(1)`, indexing is `O(1)`.
- `collections.deque` → double-ended queue backed by a linked list; fast appends/pops from both ends.
- `dict` / `set` → hash tables with `O(1)` average lookups.
- `heapq` → binary heap implemented over a list; `heapq.heappush` / `heappop` are `O(log n)`.

These standard types are enough to express most interview solutions concisely. When a scenario demands custom behaviour (e.g., ordered dictionary with quick minimum lookup), design your own structure or combine the primitives above.

## Interview checkpoints
- State the operations and complexity guarantees you expect before coding.
- Mention memory overhead when it affects feasibility (e.g., dense adjacency matrix vs. sparse list).
- Keep a comparison table handy so you can justify switching structures under pressure.

Planned coverage includes linear structures, hash-based containers, tree variants, graph representations, heaps, and advanced structures. Check the README data-structure outline for the up-to-date roadmap.

## Quick comparison cheat sheet

| Structure family | Core operations (amortised) | Strengths | Consider alternatives when… |
| --- | --- | --- | --- |
| Arrays / Dynamic arrays | Index `O(1)`, append `O(1)`, insert middle `O(n)` | Cache-friendly, predictable iteration, simple slicing | Frequent mid-list inserts → linked lists; bidirectional growth → deque |
| Linked lists | Insert/delete with pointer `O(1)`, search `O(n)` | Constant-time structural updates, stable iterators | Need random access or cache locality → arrays or trees |
| Stacks / Queues (`deque`) | Push/pop ends `O(1)` | Enforce LIFO/FIFO discipline, simple APIs | Require priority ordering → heaps; random removal → linked list/array |
| Hash tables / Sets | Lookup/insert/delete `O(1)` average | Fast membership, flexible keys | Need ordering/range queries → trees or skip lists; memory tight → arrays |
| Trees (BST, AVL, RB) | Lookup/insert/delete `O(log n)` | Sorted iteration, range queries, balanced guarantees | Only min/max needed → heaps; dataset lives on disk → B-trees |
| Tries | Insert/search `O(L)` | Efficient prefix queries, lexical ordering | Sparse prefixes → hash tables; huge alphabets → compressed trie |
| Graph representations | Adj. list: `O(|V| + |E|)` storage, adjacency matrix: `O(|V|^2)` | Tune to sparsity/density, friendly to traversal algorithms | Need streaming edge access → edge list; bitset for dense boolean graphs |
| Heaps / Priority queues | Push/pop `O(log n)`, peek `O(1)` | Fast priority scheduling, top-k queries | Need decrease-key heavy workloads → pairing/Fibonacci heap; ordered iteration → trees |
| Union-Find | `find/union` ≈ `O(1)` amortised | Dynamic connectivity, cycle detection | Need path queries → trees/graphs; frequent rollbacks → DSU with undo |
| Skip lists | Search/insert/delete `O(log n)` expected | Ordered set/map with simple implementation | Worst-case guarantees required → balanced trees; memory-constrained → arrays |
| Bloom filters | Insert/query `O(k)` | Memory-light membership tests, tunable false positives | False negatives unacceptable → hash set; counts/deletes needed → counting Bloom filter |
| LRU caches | `get/put` `O(1)` | Recency-based eviction, drop-in caching | Frequency matters more → LFU/ARC; capacity tiny → array/list sufficient |

Use this cheat sheet alongside individual chapters to justify structure selection during interviews.

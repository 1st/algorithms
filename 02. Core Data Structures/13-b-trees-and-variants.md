# 13 · B-Trees and Variants

B-trees generalise balanced search trees for disk and SSD storage by storing many keys per node. They minimise I/O operations, making them foundational in databases and filesystems.

## Learning objectives
- Understand node structure, branching factor, and how B-trees maintain balance
- Describe search, insert, and delete algorithms and their complexity
- Recognise where B-trees, B+ trees, and B* trees appear in real systems
- Contrast B-trees with binary balanced trees in memory vs. disk contexts

## Node structure
- Each node holds up to `m - 1` keys and `m` children (order `m`).
- Keys inside a node keep sorted order; children subtrees cover value ranges between keys.
- Root can have as few as 2 children; internal nodes (except root) must stay at least half full.

## Operations overview

| Operation | Time complexity | Notes |
| --- | --- | --- |
| Search | `O(log_m n)` node visits | Each node scan is `O(m)` but kept small; dominated by disk I/O |
| Insert | `O(log_m n)` | Splits propagate upward; ensures nodes stay within capacity |
| Delete | `O(log_m n)` | May borrow from siblings or merge nodes |
| Range scan | `O(log_m n + k)` | Sequential access within leaves |

### Search
1. Start at root; perform binary search within node keys to choose child.
2. Repeat until leaf or key found. Disk access cost depends on tree height (
`≈ log_m n`).

### Insert
1. Find leaf for key.
2. Insert key into leaf (maintaining order).
3. If node overflows (> `m - 1` keys), split around median; promote median to parent.
4. If parent overflows, repeat up the tree. Root split increases height by 1.

### Delete
1. Remove key from node (and replace with predecessor/successor if internal node).
2. If node underflows (< ⌈`(m-1)/2`⌉ keys), borrow from sibling or merge nodes.
3. Adjust parent keys accordingly; can cascade up to root.

## B+ trees and B* trees
- **B+ tree:** stores all actual keys in leaves; internal nodes hold routing keys only. Leaves form a linked list for fast range scans—popular in databases.
- **B* tree:** keeps nodes at least 2/3 full, redistributing entries more aggressively before splitting; improves space utilisation.

## Practical considerations
- Choose branching factor `m` so nodes match disk page or cache line sizes.
- Use prefetching/read-ahead when scanning leaves for range queries.
- Internal arrays often use binary search or finger search for in-node lookups.
- Many modern systems employ Log-Structured Merge (LSM) trees, but B-trees remain foundational knowledge.

## When to use B-trees
- Handling datasets larger than main memory (databases, filesystems).
- Need ordered iteration and range queries with minimal disk seeks.
- Implementing indexes where branching factor can be tuned to hardware characteristics.

## When to look elsewhere
- In-memory workloads with small datasets → balanced binary trees or hash tables.
- Append-heavy writes with relaxed read latency → LSM trees.
- Need probabilistic membership → Bloom filters or Cuckoo filters.

## Interview checkpoints
- Explain why B-trees minimize disk I/O (high branching factor lowers height).
- Describe node splitting and merging succinctly, focusing on invariants.
- Mention the ubiquity of B+ trees in relational databases and storage engines.

## Further practice
- Walk through sample insert/delete sequences to track splits/merges.
- Implement a simplified B-tree in Python for intuition (fixed small `m`).
- Explore how database indexes expose B-tree properties (clustered vs. non-clustered).

# 11 · Balanced Search Trees

Balanced search trees keep height near `O(log n)` regardless of insertion order. They guarantee predictable performance for search, insert, delete, and range queries—critical for interview scenarios demanding worst-case guarantees.

## Learning objectives
- Understand the balancing strategies behind AVL and Red-Black trees
- Describe rotations and how they restore invariants after updates
- Compare balanced trees to BSTs, heaps, and other structures
- Recognise when to reach for order-augmented variants (order statistics, interval queries)

## Why balance matters
- Unbalanced BST height can reach `n`, degrading operations to `O(n)`.
- Balanced trees maintain height `≈ log₂(n)` by rebalancing during insert/delete.
- They support ordered operations (inorder traversal) and range queries efficiently.

## AVL trees (Adelson-Velsky and Landis)
- Strict balance: heights of left and right subtrees differ by at most 1.
- Store height or balance factor at each node.
- Rebalancing involves single or double rotations after insert/delete.

### Rotations
- **Single right rotation (LL case):**
  ```
      y            x
     / \          / \
    x   C  →     A   y
   / \              / \
  A   B            B   C
  ```
- **Right-left (RL) or left-right (LR) cases:** perform two rotations.

## Red-Black trees
- Looser balance: heights differ by at most ~2× log₂(n), but simpler invariants.
- Nodes are red or black; root is black; red nodes have black children; every path has same number of black nodes.
- Insertions and deletions recolor and rotate to maintain properties.
- Widely used in standard libraries (e.g., `std::map`, Java’s `TreeMap`).

## B-trees preview
- Generalisation of balanced trees for secondary storage (covered separately). Allow many children per node to minimise disk I/O.

## Operations complexities

| Operation | Balanced trees (`n` nodes) |
| --- | --- |
| Lookup | `O(log n)` |
| Insert | `O(log n)` |
| Delete | `O(log n)` |
| Range query (k outputs) | `O(log n + k)` |

## Augmentations
- **Order-statistic tree:** store subtree sizes to support `k`-th element queries.
- **Interval tree:** store interval endpoints and max values for overlap searches.
- **Segment tree / Fenwick tree:** array-like augmentations for range sums (covered elsewhere).

## When to choose balanced trees
- Need sorted iteration with guaranteed `O(log n)` updates.
- Performing range queries, predecessor/successor lookups, or maintaining dynamic ordered sets.
- Requiring worst-case guarantees under adversarial inputs.

## When to look elsewhere
- Prioritise constant-time lookups and order is irrelevant → hash tables.
- Need frequent min/max only → heaps.
- Handling disk-resident data → B-trees or LSM trees.

## Interview checkpoints
- Explain rotation sequences clearly; consider sketching diagrams.
- Mention that many languages offer balanced trees in the standard library; knowing their behaviour suffices.
- Discuss trade-offs between AVL (stricter balance, faster lookups) and Red-Black (fewer rotations, faster inserts).

## Further practice
- Implement AVL insert/delete with rotations to gain intuition.
- Explore Red-Black tree insertion cases to understand recoloring.
- Build an order-statistic tree by augmenting nodes with subtree size.

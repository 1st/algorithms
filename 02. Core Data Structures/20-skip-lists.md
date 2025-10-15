# 20 · Skip Lists

Skip lists maintain multiple levels of linked lists to achieve expected `O(log n)` search, insert, and delete without complex rotations. They offer probabilistic balancing and are easier to implement than balanced trees.

## Learning objectives
- Understand skip list structure and how express lanes accelerate search
- Implement search, insert, and delete with probabilistic level assignment
- Compare skip lists to balanced trees and hash tables in terms of guarantees
- Recognise practical use cases (in-memory indexes, ordered maps)

## Structure overview
- Base level (level 0) contains all elements in sorted order linked list.
- Each higher level contains a subset of elements, forming “express lanes.”
- Promotion probability `p` (commonly 0.5) determines expected height `O(log n)`.

## Node representation

```python
import random

class SkipNode:
    def __init__(self, value, level):
        self.value = value
        self.forward = [None] * (level + 1)


class SkipList:
    def __init__(self, p=0.5, max_level=16):
        self.p = p
        self.max_level = max_level
        self.header = SkipNode(None, max_level)
        self.level = 0

    def random_level(self) -> int:
        lvl = 0
        while random.random() < self.p and lvl < self.max_level:
            lvl += 1
        return lvl
```

## Operations
- **Search:** Start at highest level; move right while next value < target; drop down a level when you can’t advance.
- **Insert:** Use update pointers per level, generate random level, splice node into forward pointers.
- **Delete:** Similar to insert; adjust forward pointers where node appears.

```python
    def search(self, value):
        node = self.header
        for lvl in reversed(range(self.level + 1)):
            while node.forward[lvl] and node.forward[lvl].value < value:
                node = node.forward[lvl]
        node = node.forward[0]
        return node and node.value == value
```

- Expected time for search/insert/delete: `O(log n)`.
- Space: `O(n)` expected due to geometric distribution of promotions.

## Comparison
- **Balanced BST:** deterministic `O(log n)`; more complex rotations.
- **Skip list:** probabilistic `O(log n)`; simple pointer operations.
- **Hash table:** `O(1)` average but no ordering; skip lists maintain sorted order.

## Use cases
- Ordered maps/sets in systems like Redis (sorted sets).
- In-memory indexes where predictability and simplicity matter.
- Concurrent structures (lock-free variants exist).

## Interview checkpoints
- Be prepared to explain the probability mechanism and expected vs. worst-case (`O(n)`).
- Show the search path visually (levels and express lanes).
- Mention that skip lists can support range queries by walking level 0.

## Further practice
- Implement full insert/delete logic and test with random data.
- Compare search times against balanced trees and arrays for large `n`.
- Explore deterministic skip lists (skip search lists) using fixed promotion rules.

# 03 · Linked Lists

Linked lists trade contiguous storage for flexible insertion and removal. Nodes point to one another, allowing structural updates without mass shifts—at the cost of slower random access.

## Learning objectives
- Distinguish singly vs. doubly linked lists and identify common variants
- Recall operation complexities and why pointer chasing can hurt performance
- Implement core operations (insert, delete, reverse) safely in Python
- Decide when the benefits of O(1) insertion/deletion outweigh cache costs

## Operations quick reference

| Operation | Singly linked list | Doubly linked list | Notes |
| --- | --- | --- | --- |
| Access by index | `O(n)` | `O(n)` | Must traverse from head (or tail for DLL) |
| Insert/delete at head | `O(1)` | `O(1)` | Update head (and possibly tail for empty lists) |
| Insert/delete at tail | `O(n)` (unless tail pointer) | `O(1)` with tail pointer | Maintaining a tail pointer avoids full traversal |
| Insert/delete in middle (known node) | `O(1)` | `O(1)` | Need pointer to predecessor (singly) or node itself (doubly) |
| Search by value | `O(n)` | `O(n)` | Linear scan |

### Sentinel nodes
Dummy head/tail nodes simplify edge cases (empty list, single element). They reduce conditionals when inserting or removing at boundaries.

## Python implementation notes

```python
from dataclasses import dataclass
from typing import Optional, Iterable, Iterator, TypeVar, Generic

T = TypeVar("T")

@dataclass
class Node(Generic[T]):
    value: T
    next: Optional["Node[T]"] = None


class SinglyLinkedList(Generic[T]):
    def __init__(self, values: Iterable[T] = ()):
        self.head: Optional[Node[T]] = None
        for value in values:
            self.prepend(value)

    def prepend(self, value: T) -> None:
        self.head = Node(value, next=self.head)

    def __iter__(self) -> Iterator[T]:
        current = self.head
        while current:
            yield current.value
            current = current.next
```

- Python has no built-in linked list; `collections.deque` uses a doubly linked list under the hood.
- Use `dataclasses` to define nodes succinctly; ensure you avoid default mutable arguments.
- Guard against losing references when deleting nodes—update predecessor pointers carefully.

## Variants and extensions
- **Circular lists:** last node points back to head; useful for round-robin scheduling.
- **Skip lists:** layered linked lists granting logarithmic search through probabilistic express lanes.
- **Unrolled linked lists:** store small arrays per node to reduce pointer overhead.

## When to choose linked lists
- Frequent insertions/deletions at arbitrary positions where you already hold node references.
- Need stable iterators (pointers remain valid after modifications).
- Building adjacency chains where memory fragmentation is acceptable.

## When to look elsewhere
- Need fast random access—arrays or balanced trees win.
- Working in languages with poor cache locality impacts; linked lists incur pointer chasing.
- Prioritise memory compactness—per-node overhead can be significant.

## Interview checkpoints
- Explain why search is `O(n)` and articulate cache-locality costs.
- Demonstrate node insertion/deletion without memory leaks (or describe GC handling in Python).
- Contrast singly vs. doubly linked lists: extra pointer buys O(1) deletion when node pointer known.

## Further practice
- Implement list reversal iteratively and recursively.
- Build a queue backed by a linked list to observe pointer updates.
- Explore skip list basics as a bridge into advanced probabilistic structures.

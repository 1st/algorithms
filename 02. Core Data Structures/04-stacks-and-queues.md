# 04 · Stacks and Queues

Stacks and queues encode disciplined access patterns—last-in-first-out and first-in-first-out—that simplify many algorithmic problems, from DFS traversal to task scheduling.

## Learning objectives
- Describe stack vs. queue semantics and typical operation sets
- Use Python-native structures (`list`, `deque`, `queue`) to implement stacks/queues efficiently
- Recognise canonical problems solvable with each abstraction
- Understand complexity considerations for enqueue/dequeue operations under different backings

## Operations quick reference

| Structure | Core operations | Python implementation | Complexity |
| --- | --- | --- | --- |
| Stack (LIFO) | `push`, `pop`, `peek`, `is_empty` | `list.append`, `list.pop` | `O(1)` amortised |
| Queue (FIFO) | `enqueue`, `dequeue`, `peek`, `is_empty` | `collections.deque.append`, `popleft` | `O(1)` |
| Queue (FIFO, simple) | `list.append`, `pop(0)` | `list` | `enqueue O(1)`, `dequeue O(n)` due to shifting |
| Double-ended queue | append left/right, pop left/right | `collections.deque` | `O(1)` |

### Choosing the backing store
- `collections.deque` is a doubly linked list with block storage, optimised for append/pop operations at both ends.
- Avoid using `list.pop(0)` for queues—it shifts every element and degrades performance.
- Bounded queues can be created with `deque(maxlen=n)` to auto-drop the oldest entries.

## Python implementation notes

```python
from collections import deque

def bfs_levels(root) -> list[list[int]]:
    if root is None:
        return []
    levels: list[list[int]] = []
    queue: deque[tuple["Node", int]] = deque([(root, 0)])
    while queue:
        node, depth = queue.popleft()
        if depth == len(levels):
            levels.append([])
        levels[depth].append(node.value)
        for child in node.children:
            queue.append((child, depth + 1))
    return levels
```

- Stacks can use Python lists (`append`, `pop`). `deque` also works and avoids occasional resizing.
- For multi-producer/multi-consumer scenarios, prefer `queue.Queue` (thread-safe) or `asyncio.Queue`.
- Use `deque` for sliding-window problems to maintain extremal values in `O(n)` total time.

## Canonical use cases
- **Stacks:** DFS traversal, backtracking, expression evaluation (parentheses matching, RPN), undo functionality.
- **Queues:** BFS traversal, level-order traversal, scheduling tasks, buffering streams.
- **Double-ended queues:** Sliding window maxima/minima, palindromic checks, time-based caches.

## Variants
- **Min/Max stack:** store pairs `(value, current_min)` to track extremal values in `O(1)`.
- **Priority queue:** separate abstraction covered in the Heaps section.
- **Circular buffers:** array-backed queues with head/tail indices for fixed-size streaming.

## Interview checkpoints
- Articulate why `deque` provides `O(1)` dequeue while `list.pop(0)` does not.
- Show how to convert recursion into an explicit stack to avoid call-stack limits.
- Highlight queue-based level traversal vs. stack-based depth traversal for tree/graph problems.

## Further practice
- Implement an iterative binary tree inorder traversal using a stack.
- Solve sliding window maximum using a monotonic deque.
- Build a fixed-capacity circular queue and handle wrap-around indexing.

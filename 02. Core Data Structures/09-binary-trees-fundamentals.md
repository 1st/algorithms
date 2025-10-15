# 09 · Binary Trees Fundamentals

Binary trees underpin many interview questions and advanced data structures. A solid grasp of traversal orders, recursion patterns, and structural properties sets the stage for BSTs, heaps, and tries.

## Learning objectives
- Describe binary tree terminology (height, depth, leaf, internal node, balanced)
- Traverse trees using preorder, inorder, postorder, and level-order techniques
- Implement recursive and iterative traversals safely in Python
- Analyse time/space complexity for traversal, search, and update operations

## Node representation

```python
from dataclasses import dataclass
from typing import Optional, TypeVar, Generic, Iterable

T = TypeVar("T")

@dataclass
class BinaryTreeNode(Generic[T]):
    value: T
    left: Optional["BinaryTreeNode[T]"] = None
    right: Optional["BinaryTreeNode[T]"] = None
```

## Traversal patterns

| Order | Visit sequence | Typical uses |
| --- | --- | --- |
| Preorder (`root → left → right`) | Process node before children | Serialize tree, copy structure |
| Inorder (`left → root → right`) | Process left subtree, node, right | Sorted output for BSTs |
| Postorder (`left → right → root`) | Process children before node | Delete tree, evaluate expressions |
| Level-order (BFS) | Traverse by depth | Shortest path in unweighted tree, level grouping |

### Recursive inorder example

```python
def inorder(node: Optional[BinaryTreeNode[int]]) -> list[int]:
    if not node:
        return []
    return inorder(node.left) + [node.value] + inorder(node.right)
```

### Iterative inorder with stack

```python
def inorder_iterative(root: Optional[BinaryTreeNode[int]]) -> list[int]:
    result: list[int] = []
    stack: list[BinaryTreeNode[int]] = []
    current = root
    while current or stack:
        while current:
            stack.append(current)
            current = current.left
        current = stack.pop()
        result.append(current.value)
        current = current.right
    return result
```

## Complexity reference
- Traversal (DFS/BFS): `O(n)` time, `O(h)` space for recursion/stack (`h` = height).
- Search (generic binary tree): `O(n)` worst-case unless extra structure (BST).
- Insert/delete: structure-dependent—basic binary tree insertion often follows domain-specific constraints (e.g., heap, BST rules).

## Structural properties
- **Height:** longest path from node to leaf; balanced trees aim for `O(log n)` height.
- **Complete tree:** all levels filled except possibly the last, which is left-filled.
- **Full tree:** every node has either 0 or 2 children.
- **Perfect tree:** both complete and full; `n = 2^{h+1} - 1`.

## Interview checkpoints
- Explain traversal orders and choose the right one for a problem (e.g., inorder for sorted output).
- Reason about recursion depth and convert to iterative versions when stack limits are a concern.
- Recognise when an unbalanced tree degenerates to a linked list, impacting complexity.

## Further practice
- Implement serialization/deserialization (e.g., LeetCode’s tree encoding).
- Solve tree diameter, LCA, and maximum path sum problems using DFS.
- Write level-order traversal that groups values per depth for BFS familiarity.

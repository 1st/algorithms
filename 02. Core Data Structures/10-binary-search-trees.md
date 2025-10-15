# 10 · Binary Search Trees

Binary Search Trees (BSTs) enforce ordering constraints so that left descendants hold smaller keys and right descendants hold larger keys. This property enables efficient search, insert, and delete—provided the tree remains balanced.

## Learning objectives
- Maintain BST invariants during lookup, insertion, and deletion
- Analyse expected vs. worst-case complexities and the role of balancing
- Implement classic operations (search, insert, delete, successor) in Python
- Recognise when to choose BSTs over hash tables or arrays

## Operations quick reference

| Operation | Average complexity | Worst case (skewed) | Notes |
| --- | --- | --- | --- |
| Lookup | `O(log n)` | `O(n)` | Depends on tree height |
| Insert | `O(log n)` | `O(n)` | Maintains structure by comparing keys |
| Delete | `O(log n)` | `O(n)` | Handle 0, 1, or 2-child cases |
| Find min/max | `O(log n)` | `O(n)` | Walk left/right pointers |
| Inorder traversal | `O(n)` | `O(n)` | Outputs sorted keys |

## Core operations

```python
def search(node: Optional[BinaryTreeNode[int]], key: int) -> Optional[BinaryTreeNode[int]]:
    while node:
        if key < node.value:
            node = node.left
        elif key > node.value:
            node = node.right
        else:
            return node
    return None


def insert(node: Optional[BinaryTreeNode[int]], key: int) -> BinaryTreeNode[int]:
    if node is None:
        return BinaryTreeNode(key)
    if key < node.value:
        node.left = insert(node.left, key)
    elif key > node.value:
        node.right = insert(node.right, key)
    return node
```

### Delete cases
1. **Leaf node:** remove directly.
2. **One child:** replace node with its child.
3. **Two children:** replace value with inorder successor (smallest in right subtree) or predecessor and delete that node recursively.

```python
def delete(node: Optional[BinaryTreeNode[int]], key: int) -> Optional[BinaryTreeNode[int]]:
    if not node:
        return None
    if key < node.value:
        node.left = delete(node.left, key)
    elif key > node.value:
        node.right = delete(node.right, key)
    else:
        if not node.left:
            return node.right
        if not node.right:
            return node.left
        successor = node.right
        while successor.left:
            successor = successor.left
        node.value = successor.value
        node.right = delete(node.right, successor.value)
    return node
```

## Balanced vs. unbalanced
- **Balanced BSTs** maintain height close to `O(log n)` (e.g., AVL, Red-Black). Insert/delete cost remains logarithmic.
- **Unbalanced BSTs** can devolve into linked lists if inserts are sorted or adversarial (`O(n)` height). Randomized insertions help maintain average balance.

## When to choose BSTs
- Need ordered iteration plus searches/inserts better than `O(n)`.
- Require predecessor/successor queries (e.g., floor/ceil operations).
- Need to maintain dynamic sets/subsets with range queries.

> **Interview tip:** Draw a quick diagram showing left < root < right when explaining BST invariants—visuals demonstrate clarity faster than words.

## When to look elsewhere
- Strict `O(1)` lookups matter more than ordering → hash tables.
- Heavy range queries or segment operations → augmented trees/fenwick trees.
- Frequent min/max retrieval without ordering → heaps.

> **Common pitfall:** Forgetting to handle duplicate keys. Clarify policy (“I’ll store duplicates on the right subtree” or “I’ll keep a count field”) before coding.

## Interview checkpoints
- Explain delete scenarios clearly; many candidates struggle with the two-child case.
- Discuss how insertion order affects performance and how self-balancing variants fix it.
- Mention augmentations (storing subtree sizes or sums) to answer order-statistics queries.

## Further practice
- Implement BST validation (check invariants).
- Add methods for `lower_bound`/`upper_bound` (successor/predecessor).
- Explore randomised BSTs (treaps) as a bridge to balanced trees.

# 12 · Tries and Prefix Trees

Tries (prefix trees) store strings character by character, enabling fast prefix searches, autocomplete, and dictionary-based pattern matching. They trade memory for predictable lookup depth proportional to key length.

## Learning objectives
- Represent trie nodes and transitions effectively in Python
- Implement insert, search, and prefix queries with linear complexity in key length
- Recognise space/time trade-offs between tries, hash tables, and trees
- Extend tries with metadata (counts, end-of-word flags, suggestions)

## Node representation

```python
from dataclasses import dataclass, field
from typing import Dict, Optional

@dataclass
class TrieNode:
    children: Dict[str, "TrieNode"] = field(default_factory=dict)
    is_word: bool = False
    freq: int = 0  # optional metadata (e.g., word frequency)
```

## Core operations

```python
class Trie:
    def __init__(self):
        self.root = TrieNode()

    def insert(self, word: str) -> None:
        node = self.root
        for ch in word:
            if ch not in node.children:
                node.children[ch] = TrieNode()
            node = node.children[ch]
        node.is_word = True
        node.freq += 1

    def search(self, word: str) -> bool:
        node = self.root
        for ch in word:
            node = node.children.get(ch)
            if node is None:
                return False
        return node.is_word

    def starts_with(self, prefix: str) -> bool:
        node = self.root
        for ch in prefix:
            node = node.children.get(ch)
            if node is None:
                return False
        return True
```

## Complexity
- Insert/search/prefix: `O(L)` where `L` is word length.
- Space: `O(Σ L)` for all strings; higher than hash tables due to per-character nodes.

## Optimisations and variants
- **Compressed trie (radix tree):** merge chains of single-child nodes into multi-character edges to reduce memory.
- **Ternary search tree:** hybrid of BST and trie that stores characters in nodes with three pointers (less memory).
- **Wildcard/pattern search:** augment nodes to handle special characters or regex-like queries.
- **Autocomplete:** store top-k suggestions or counts per node to guide recommendation.

## When to use tries
- Need to support prefix queries or lexicographic traversal efficiently.
- Datasets share long common prefixes (e.g., dictionary words, URLs).
- Want to avoid hash collisions or inconsistent ordering from hash tables.

## When to look elsewhere
- Keys are random with little prefix sharing → hash tables more memory-efficient.
- Need ordered iteration but not prefix operations → balanced BST.
- Very large alphabets (Unicode) → consider compressed tries or hashed child maps.

## Interview checkpoints
- State `O(L)` complexity and contrast with hash-table lookups.
- Discuss memory overhead and how compressed tries mitigate it.
- Explain extensions like storing end-of-word flags or counts for frequency analysis.

## Further practice
- Build autocomplete returning top suggestions based on stored frequencies.
- Solve word-search problems using tries combined with DFS over boards.
- Implement suffix trie or suffix array as stepping stones toward advanced string algorithms.

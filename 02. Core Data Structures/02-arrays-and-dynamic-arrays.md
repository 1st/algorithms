# 02 · Arrays and Dynamic Arrays

Dynamic arrays back most high-level “list” abstractions. They offer contiguous storage, predictable iteration, and efficient amortised appends—ideal defaults for interview solutions.

## Learning objectives
- Differentiate fixed arrays from dynamic arrays and understand resizing mechanics
- Recall key operation complexities (indexing, insert/delete at ends vs. middle)
- Leverage Python’s `list` effectively while recognizing its underlying trade-offs
- Spot scenarios where you should reach for another structure instead

## Operations quick reference

| Operation | Python list method | Complexity | Notes |
| --- | --- | --- | --- |
| Index / update by position | `a[i]`, `a[i] = x` | `O(1)` | Direct pointer arithmetic into contiguous storage |
| Append to end | `a.append(x)` | Amortised `O(1)` | Occasional resize doubles capacity |
| Pop from end | `a.pop()` | `O(1)` | No shift required |
| Insert at arbitrary index | `a.insert(i, x)` | `O(n)` | Needs to shift suffix to make room |
| Delete from middle | `del a[i]` | `O(n)` | Compacts suffix to fill the gap |
| Slice copy | `a[i:j]` | `O(k)` | Proportional to slice length |

### Resizing insight
Dynamic arrays grow by allocating a larger block (commonly 2× the current capacity), copying existing elements, and releasing the old block. Amortisation keeps overall append cost near constant even though occasional resizes cost `O(n)`.

## Python implementation notes

```python
def build_prefix_sums(values: list[int]) -> list[int]:
    prefix = [0] * (len(values) + 1)
    for i, val in enumerate(values, start=1):
        prefix[i] = prefix[i - 1] + val
    return prefix
```

- Preallocate with `[0] * n` when you know the size to avoid repeated reallocations.
- `list.extend(iterable)` appends many items efficiently (amortised `O(k)`).
- Use list comprehensions for linear transformations—they are faster than appending inside a loop.

## When to choose arrays
- Need constant-time random access or tight cache locality (e.g., DP tables, binary search).
- Working set fits in memory and you want predictable iteration order.
- Frequent appends at the tail with rare mid-list insertions/removals.

## When to look elsewhere
- Heavy insert/delete in the middle → consider linked lists or balanced trees.
- Need to grow at both ends with `O(1)` cost → prefer `collections.deque`.
- Dataset may outgrow RAM → stream from disk or use generator-based pipelines.

## Interview checkpoints
- Explain amortised analysis for append operations; mention doubling strategy.
- State that inserting at the front is `O(n)` because each element shifts right.
- Relate contiguous storage to better cache utilisation compared with pointer-based structures.

## Further practice
- Implement your own minimal dynamic array class with explicit resize logic.
- Solve prefix-sum or sliding-window interview problems emphasising array indexing.
- Experiment with benchmarking `append` vs. `insert(0, x)` to feel the complexity difference.

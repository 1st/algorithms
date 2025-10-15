# 02 · Divide and Conquer

Divide and conquer breaks problems into subproblems, solves them independently, and combines their results. It underpins algorithms like merge sort, quicksort, and fast exponentiation.

## Learning objectives
- Recognise when a problem decomposes naturally into smaller subproblems
- Analyse recurrence relations using the Master Theorem or recursion trees
- Implement merge sort and quickselect in Python to internalise the pattern
- Understand trade-offs between divide-and-conquer and iterative approaches

## Template
1. **Divide:** split input into subproblems.
2. **Conquer:** solve subproblems recursively.
3. **Combine:** merge results into final answer.

## Example: Merge sort

```python
def merge_sort(values: list[int]) -> list[int]:
    if len(values) <= 1:
        return values[:]
    mid = len(values) // 2
    left = merge_sort(values[:mid])
    right = merge_sort(values[mid:])
    return merge(left, right)


def merge(a: list[int], b: list[int]) -> list[int]:
    i = j = 0
    merged: list[int] = []
    while i < len(a) and j < len(b):
        if a[i] <= b[j]:
            merged.append(a[i]); i += 1
        else:
            merged.append(b[j]); j += 1
    merged.extend(a[i:])
    merged.extend(b[j:])
    return merged
```

- Recurrence: `T(n) = 2T(n/2) + O(n)` → `O(n log n)`.
- Stable sort; `O(n)` auxiliary space.

## Example: Quickselect (select k-th smallest)

```python
import random

def quickselect(values: list[int], k: int) -> int:
    pivot = random.choice(values)
    lows = [x for x in values if x < pivot]
    highs = [x for x in values if x > pivot]
    pivots = [x for x in values if x == pivot]
    if k < len(lows):
        return quickselect(lows, k)
    if k < len(lows) + len(pivots):
        return pivots[0]
    return quickselect(highs, k - len(lows) - len(pivots))
```

- Expected `O(n)` time; worst-case `O(n²)` without careful pivot selection.

## Master theorem refresher
For recurrences `T(n) = aT(n/b) + f(n)`:
- If `f(n) = O(n^{log_b a - ε})`, then `T(n) = Θ(n^{log_b a})`.
- If `f(n) = Θ(n^{log_b a} log^k n)`, then `T(n) = Θ(n^{log_b a} log^{k+1} n)`.
- If `f(n) = Ω(n^{log_b a + ε})` and regularity holds, `T(n) = Θ(f(n))`.

## Applications
- Sorting (merge sort, quicksort).
- Searching (binary search, quickselect).
- Matrix multiplication (Strassen, divide & conquer convolution).
- Computational geometry (closest pair of points).

## When to use divide and conquer
- Problem splits evenly with minimal overlap and merge is efficient.
- Need asymptotic improvements over naive `O(n²)` approaches (e.g., merge sort vs. bubble sort).
- Recursive structure matches problem domain (tree algorithms).

## Interview checkpoints
- State recurrence and apply Master Theorem for complexity.
- Discuss space usage (call stack and temporary buffers).
- Mention tail recursion elimination or iterative conversions when helpful.

## Further practice
- Implement binary search variants (first/last occurrence) using recursive templates.
- Solve closest pair of points or maximum subarray via divide and conquer.
- Explore convolution via FFT as an advanced application.

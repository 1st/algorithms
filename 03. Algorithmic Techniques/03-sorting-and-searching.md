# 03 · Sorting and Searching

Sorting organizes data for efficient querying; searching retrieves data quickly from structured collections. Mastering key algorithms provides a toolkit for array and list manipulation in interviews.

## Learning objectives
- Compare time/space complexity and stability of common sorting algorithms
- Choose appropriate searching techniques (binary search variants, exponential search)
- Implement typical interview-friendly patterns (two pointers, sliding window over sorted data)
- Recognize when to leverage library sorts vs. custom algorithms

## Sorting algorithms overview

| Algorithm | Time (best/avg/worst) | Space | Stable | Notes |
| --- | --- | --- | --- | --- |
| Bubble / Insertion | `O(n) / O(n²) / O(n²)` | `O(1)` | Yes | Simple, use for nearly sorted data |
| Merge sort | `O(n log n)` | `O(n)` | Yes | Divide & conquer, external sorting |
| Quick sort | `O(n log n) / O(n²)` | `O(log n)` stack | No (default) | In-place average fast, pivot choice critical |
| Heap sort | `O(n log n)` | `O(1)` | No | Uses binary heap; predictable but not stable |
| Counting/Radix sort | `O(n + k)` | `O(k)` | Yes | When key range small or fixed-width digits |

Python’s `sort()` / `sorted()` use Timsort (hybrid merge/insertion), stable `O(n log n)` with `O(n)` worst-case space.

## Binary search patterns

```python
def binary_search(values: list[int], target: int) -> int:
    left, right = 0, len(values) - 1
    while left <= right:
        mid = (left + right) // 2
        if values[mid] < target:
            left = mid + 1
        elif values[mid] > target:
            right = mid - 1
        else:
            return mid
    return -1
```

- Variants: first occurrence, last occurrence, lower/upper bound (bisect).
- Works on monotonic predicates: `while left < right: mid = (left + right) // 2`.

### Exponential search
When array length unknown or unbounded, expand search interval exponentially before binary searching portion.

## Two-pointer technique
- Requires sorted arrays/lists or specific structure.
- Use to find pairs/triples meeting sum constraints, merge intervals, remove duplicates.
- Sliding window (expand right pointer, contract left) suits positive ranges or strings.

## When to sort
- To enable binary search and two-pointer patterns.
- To canonicalize data for hashing or comparing (e.g., anagram grouping).
- To minimize objective functions (interval scheduling, greedy heuristics).

## Interview checkpoints
- Justify algorithm choice with data characteristics (size, constraints, distribution).
- Mention stability requirements when relevant (merging logs, maintaining order of equal values).
- Discuss trade-offs of pre-sorting vs. on-the-fly processing (time vs. space).

## Further practice
- Implement quicksort with random pivot and tail recursion elimination.
- Solve “search rotated sorted array”, “find k closest elements”, and sliding window problems.
- Use `bisect` module to maintain sorted lists efficiently.

# 02 · Big-O Cheat Sheet

Quick reference for common complexities, practical thresholds, and algorithm examples. Use this sheet to evaluate solutions on the fly.

## Growth rates (slowest → fastest)

| Complexity | Notes | Example algorithms / operations |
| --- | --- | --- |
| `O(1)` constant | Independent of input size | Hash table lookup, array indexing |
| `O(log n)` logarithmic | Each step halves problem | Binary search, heap push/pop |
| `O(n)` linear | Visits each element once | Array scan, hashmap iteration |
| `O(n log n)` linearithmic | Common optimal sort bound | Merge sort, heap sort, balanced BST operations |
| `O(n²)` quadratic | Doubly nested loops | Matrix multiplication (naive), bubble sort |
| `O(n³)` cubic | Triple nested loops | Floyd-Warshall, 3D DP |
| `O(2^n)` exponential | Explore all subsets/choices | Naive recursion for subset problems |
| `O(n!)` factorial | All permutations | Travelling salesman brute force |

## Practical limits (rule of thumb)

| Input size (`n`) | Acceptable complexity |
| --- | --- |
| ≤ 10^2 | Up to `O(n³)` or `O(2^n)` with pruning |
| ≤ 10^3 | `O(n²)` safe, `O(n³)` borderline |
| ≤ 10^5 | `O(n log n)` or better |
| ≤ 10^7 | `O(n)` or `O(log n)` |
| ≥ 10^9 | Usually requires `O(1)` per query, mathematical derivation, or streaming |

## Space complexity cues
- `O(1)` auxiliary space: in-place algorithms (two pointers, heap sort).
- `O(n)` space: storing copies, DP arrays, recursion stack.
- `O(n²)` space: DP tables, adjacency matrices; watch memory usage.
- Recursion depth equals maximum call stack; Python default recursion limit ≈ 1000.

## Complexity by data structure
- **Array / list:** indexing `O(1)`, append `O(1)` amortised, insert middle `O(n)`.
- **Linked list:** insert/delete `O(1)` with pointer, lookup `O(n)`.
- **Hash table (`dict`, `set`):** average `O(1)` operations; worst `O(n)` with collisions.
- **Balanced BST:** lookup/insert/delete `O(log n)`.
- **Heap:** push/pop `O(log n)`, peek `O(1)`.
- **Trie:** lookup `O(L)` for key length `L`.

## Sorting cheats
- **Stable:** merge sort, insertion sort, Timsort (Python). Use when equal elements must preserve order.
- **In-place:** quicksort, heap sort (not stable), insertion sort.
- **Counting/Radix sort:** `O(n + k)` when key range `k` small/known.

## Recurrence patterns (Master theorem)
- `T(n) = 2T(n/2) + O(n)` → `O(n log n)` (merge sort).
- `T(n) = T(n/2) + O(1)` → `O(log n)` (binary search).
- `T(n) = T(n - 1) + O(1)` → `O(n)` (linear recursion).
- `T(n) = 2T(n-1) + O(1)` → `O(2^n)` (subset recursion).

## Memory conversions
- 1 KB ≈ 10^3 bytes, 1 MB ≈ 10^6 bytes, 1 GB ≈ 10^9 bytes.
- `int` in Python is unbounded but overhead ~28 bytes; lists hold references (~8 bytes per pointer).
- Be cautious with `n²` structures when `n` > 10^4 (`10^8` entries ≈ hundreds of MB).

## Quick decision checklist
- What is `n` (and other dimensions)?
- Is an `O(n log n)` sort acceptable, or do you need linear time?
- Are there multiple inputs (`n` vs. `m`)? Express complexity accordingly (e.g., `O(n + m)`).
- Do memory constraints forbid `O(n)` extra storage?
- Could we leverage problem structure (sorted input, bounded range, monotonic predicate)?

Print or keep this cheat sheet handy to sanity-check solutions during interviews.

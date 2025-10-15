# 04 · Complexity Basics

Complexity analysis is the language we use to reason about the cost of an algorithm before we benchmark it. You do not need calculus to be effective—you need a small vocabulary, a few patterns, and a habit of asking “how does this scale?”

## Learning objectives
- Read and communicate Big-O, Big-Θ, and Big-Ω notation with confidence
- Recognise common complexity classes and what they feel like in production
- Break down loops and recursive calls into cost expressions you can compare

## Key definitions
- **Time complexity:** how the runtime grows as input size increases.
- **Space complexity:** how the memory footprint grows with input size.
- **Big-O (`O`):** an upper bound—“runtime grows no faster than…”.
- **Big-Ω (`Ω`):** a lower bound—“runtime grows at least as fast as…”.
- **Big-Θ (`Θ`):** a tight bound—both Big-O and Big-Ω hold.

We mostly use Big-O in interviews because proving the upper bound is often enough to compare strategies quickly.

## Common growth classes
- `O(1)` constant: hash lookups, array indexing.
- `O(log n)` logarithmic: binary search, balanced BST insert.
- `O(n)` linear: scanning a list once.
- `O(n log n)` linearithmic: efficient sorts (merge/quick sort average case).
- `O(n²)` quadratic: brute-force pair comparisons.
- `O(2ⁿ)` exponential: naive subset generation, some recursion without pruning.

Knowing the shape helps you predict when an algorithm will stop being practical.

## Worked comparison
Revisit the maximum pairwise product example. Count the core operations in each approach:

```python
def bruteforce(values: list[int]) -> int:
    best = float("-inf")
    for i in range(len(values)):
        for j in range(i + 1, len(values)):
            best = max(best, values[i] * values[j])  # executes ~n²/2 times
    return int(best)


def linear_scan(values: list[int]) -> int:
    first, second = sorted(values[:2])
    for candidate in values[2:]:
        if candidate >= first:
            first, second = candidate, first
        elif candidate > second:
            second = candidate
    return first * second
```

- `bruteforce` touches roughly `n²/2` pairs. Double `n`, you quadruple the work.
- `linear_scan` touches each element once: double `n`, you double the work.

The difference is invisible for short lists and life-changing for inputs in the millions.

## Checklist for future problems
- Identify the dominant operations (loops, recursion, expensive library calls).
- Express the cost in terms of the input size (`n`, `m`, etc.).
- Remove lower-order terms and constants; keep the part that grows fastest.
- State the result and sanity-check with small examples.

## Triangular numbers in nested loops
Nested loops that narrow the inner range on each pass form triangular sums:

```python
for i in range(n):
    for j in range(i + 1, n):
        process(i, j)
```

The first iteration executes `(n - 1)` times, the next `(n - 2)`, until the inner loop runs just once. Summing those counts produces `n(n - 1)/2`, which grows proportionally to `n²`. Recognising this pattern lets you state the complexity (`O(n²)`) without re-deriving the series every interview.

## Further reading
- [Triangular number](https://en.wikipedia.org/wiki/Triangular_number) for deeper intuition on these sums.
- CLRS (Chapter 3) for formal definitions if you want mathematical rigour.

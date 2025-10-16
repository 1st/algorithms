# 05 · Dynamic Programming

Dynamic programming (DP) solves problems by combining solutions to overlapping subproblems. It requires optimal substructure and overlapping subproblems, often implemented via memoisation (top-down) or tabulation (bottom-up).

## Learning objectives
- Distinguish between overlapping subproblems and independent divide-and-conquer
- Formulate DP states, transitions, and base cases
- Convert recursive memoised solutions to iterative tabulation for efficiency
- Analyse time/space complexity and optimize with state compression

## DP workflow
1. **Define state**: parameters that uniquely describe subproblem.
2. **Define recurrence**: relation between state and smaller states.
3. **Identify base cases**.
4. **Choose implementation**: top-down memoisation or bottom-up table.
5. **Optimise**: reduce space/time via rolling arrays, bitmasks, etc.

> **Interview tip:** Say your state out loud in a sentence (“`dp[i][j]` = min edits for prefixes of length `i` and `j`”) before coding—interviewers are listening for that clarity.

## Example: Fibonacci (memoised vs. tabulated)

```python
from functools import lru_cache

@lru_cache(maxsize=None)
def fib(n: int) -> int:
    if n <= 1:
        return n
    return fib(n - 1) + fib(n - 2)


def fib_tab(n: int) -> int:
    if n <= 1:
        return n
    prev, curr = 0, 1
    for _ in range(2, n + 1):
        prev, curr = curr, prev + curr
    return curr
```

## DP categories
- **1D DP:** Fibonacci, climbing stairs (`dp[i]` depends on previous few values).
- **2D DP:** grid paths, edit distance, knapsack (`dp[i][j]`).
- **Bitmask DP:** traveling salesman, subset problems. State space is `O(2^n)`—keep `n` within ~20–25 to stay tractable.
- **DP on trees:** rerooting techniques, counting paths, tree DP.
- **DP with monotonicity:** use deque optimization or convex hull trick.

## Example: 0/1 Knapsack

```python
def knapsack(weights: list[int], values: list[int], capacity: int) -> int:
    dp = [0] * (capacity + 1)
    for weight, value in zip(weights, values):
        for c in range(capacity, weight - 1, -1):
            dp[c] = max(dp[c], dp[c - weight] + value)
    return dp[capacity]
```

- Space-optimized from 2D to 1D by iterating capacity descending.

## When to use DP
- Recurrence with overlapping subproblems and optimal substructure.
- Counting ways, subsequence problems, scheduling with dependencies.
- Minimisation/maximisation with constraints (edit distance, matrix chain multiplication).

## Pitfalls
- Exponential state space; ensure states remain manageable.
- Memory blow-up with large DP tables; compress dimensions when possible.
- Off-by-one errors in table indices; define inclusive/exclusive boundaries.

> **Common pitfall:** Mixing up iteration order. If transitions depend on previous row, mention you’ll iterate `i` outer, `j` inner—and test with a small example to confirm.

## Interview checkpoints
- Express state and recurrence clearly before coding.
- Mention top-down vs. bottom-up trade-offs (stack depth, memo overhead).
- Discuss complexity in terms of state count × transition cost.

## Further practice
- Solve longest increasing subsequence via DP (O(n²) and O(n log n) variants).
- Implement edit distance and compare memoised vs. iterative solutions.
- Explore DP on trees (counting subtree sizes, rerooting for distances).

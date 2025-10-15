# 05 · Math Toolkit for Algorithms

Interview problems frequently lean on lightweight math—logarithms, exponent rules, combinatorics, and probability estimates. This chapter packages the essentials so you can recognise patterns quickly and avoid algebra under pressure.

## Learning objectives
- Convert between exponential and logarithmic forms and reason about base changes
- Estimate combinatorial counts and recognise when to reach for `n!`, `n choose k`, or permutations
- Apply basic probability tools (independence, expectation, union bound) during algorithm analysis
- Recall growth hierarchies (polynomial vs. exponential vs. factorial) when comparing complexities

## Logarithms at a glance
- Definition: `log_b(x)` answers “to what power must `b` be raised to get `x`?”
- Change of base: `log_b(x) = log_k(x) / log_k(b)`—swap bases using natural or base-2 logs.
- Power rule: `log_b(x^k) = k * log_b(x)`.
- Product rule: `log_b(xy) = log_b(x) + log_b(y)`.
- Common interview bases:
  - Base 2 (`log₂`) when reasoning about binary search, heaps, and balanced trees.
  - Base 10 (`log₁₀`) for back-of-the-envelope digit counts.
  - Natural log (`ln`) for continuous growth analysis; interchange via change-of-base.

### Quick estimates
- `log₂(1024) = 10`, `log₂(1e6) ≈ 20`, `log₂(1e9) ≈ 30`.
- `log₁₀(n)` ≈ number of digits `- 1`.

## Exponent rules
- Multiplication: `b^m * b^n = b^{m + n}`.
- Division: `b^m / b^n = b^{m - n}`.
- Power of a power: `(b^m)^n = b^{mn}`.
- Big-O intuition: `n^k` (polynomial) grows much slower than `c^n` (exponential); recognise when algorithms cross these thresholds.

## Combinatorics cheatsheet
- Factorial: `n! = n × (n - 1) × … × 1`. Approximate via Stirling’s formula when `n` is large: `n! ≈ sqrt(2πn) (n/e)^n`.
- Permutations (ordered selections): `P(n, k) = n! / (n - k)!`.
- Combinations (unordered selections): `C(n, k) = n! / (k!(n - k)!)`.
- Binomial identity: `Σ_{k=0}^n C(n, k) = 2^n`.

### Interview use cases
- Counting distinct paths, pairings, or subsets.
- Bounding brute-force search sizes before optimising.
- Estimating collision likelihood in hashing problems.

## Probability snippets
- **Independence:** `P(A ∩ B) = P(A) * P(B)`.
- **Union bound:** `P(A ∪ B) ≤ P(A) + P(B)`—handy for quick upper bounds.
- **Complement rule:** `P(not A) = 1 - P(A)`.
- **Linearity of expectation:** `E[X + Y] = E[X] + E[Y]` even if `X` and `Y` are dependent—useful in hashing and randomised algorithms.
- **Geometric distribution:** expected trials until first success with probability `p` is `1/p`.

## Growth hierarchy (from slowest to fastest)
```
O(1) < O(log n) < O(n) < O(n log n) < O(n²) < O(2^n) < O(n!)
```
Remember: algorithms with exponential or factorial behaviour become infeasible beyond small inputs; look for pruning or dynamic programming if you encounter them.

## Interview checkpoints
- Explain why binary search runs in `O(log n)` by relating each iteration to halving the search space.
- When counting possibilities, state whether order matters, then choose permutations vs. combinations.
- Use linearity of expectation or union bounds to estimate collision probabilities in hash or randomised structures.

## Further practice
- Work through classic counting problems (e.g., number of valid parentheses strings) and identify the combinatorial formula.
- Estimate probabilities for simple randomised algorithms (reservoir sampling, randomized quicksort pivots).
- Keep this chapter open while solving practice problems to reinforce pattern recognition.

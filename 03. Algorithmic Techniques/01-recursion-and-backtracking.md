# 01 · Recursion and Backtracking

Recursion expresses solutions by solving smaller subproblems of the same shape. Backtracking explores decision trees, pruning paths that cannot yield valid solutions. These techniques power combinatorial search, tree traversals, and divide-and-conquer algorithms.

## Learning objectives
- Identify problems that map naturally to recursive formulations
- Translate recursive definitions into Python functions with clear base cases
- Apply backtracking templates to generate permutations, combinations, and constraint-satisfying solutions
- Analyse time/space complexity, including branching factors and recursion depth

## Recursion essentials
- **Base case:** terminates recursion; ensures progress.
- **Recursive case:** reduces problem size and combines results.
- **Stack depth:** recursion depth equals input size for many problems; watch for stack overflows.

```python
def factorial(n: int) -> int:
    if n <= 1:
        return 1
    return n * factorial(n - 1)
```

### Tail recursion vs. helper recursion
Python lacks tail-call optimization; convert to iterative loops when depth threatens call-stack limits.

## Backtracking template

```python
def backtrack(path: list[int], options: list[int], results: list[list[int]]) -> None:
    if goal_condition(path):
        results.append(path.copy())
        return
    for choice in options:
        if not is_valid(choice, path):
            continue
        path.append(choice)
        backtrack(path, updated_options(path, options), results)
        path.pop()  # undo choice
```

- Maintain state (`path`, `used`, board) and undo changes on the way back.
- Prune search tree early by skipping invalid choices (e.g., partial constraints).

### Example: N-Queens

```python
def solve_n_queens(n: int) -> list[list[str]]:
    cols: set[int] = set()
    diag1: set[int] = set()  # r - c
    diag2: set[int] = set()  # r + c
    board = [["."] * n for _ in range(n)]
    solutions: list[list[str]] = []

    def place(row: int) -> None:
        if row == n:
            solutions.append(["".join(r) for r in board])
            return
        for col in range(n):
            if col in cols or (row - col) in diag1 or (row + col) in diag2:
                continue
            cols.add(col)
            diag1.add(row - col)
            diag2.add(row + col)
            board[row][col] = "Q"
            place(row + 1)
            board[row][col] = "."
            cols.remove(col)
            diag1.remove(row - col)
            diag2.remove(row + col)

    place(0)
    return solutions
```

## Complexity analysis
- For backtracking, total work ≈ `branches^depth`. Use pruning to shrink branching factor.
- Recursion depth influences stack space; track `O(depth)` memory usage.
- Memoisation (top-down DP) stores results of recursive calls to avoid recomputation.

## When to use recursion/backtracking
- Tree/graph traversal where natural recursion mirrors structure.
- Combinatorial generation (permutations, subsets, palindromic partitions).
- Constraint satisfaction (Sudoku, N-Queens, word search).

## Interview checkpoints
- Explain base cases and ensure they cover all termination paths.
- Discuss pruning strategies to keep exponential search manageable.
- Convert recursion to iterative solutions when interviewer asks for stack-friendly variant.

## Further practice
- Implement permutations using backtracking and compare with iterative approaches.
- Solve word-search and combination-sum problems to apply pruning.
- Explore memoised recursion (top-down DP) as a segue into dynamic programming.

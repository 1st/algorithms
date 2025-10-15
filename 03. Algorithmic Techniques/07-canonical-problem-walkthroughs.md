# 07 · Canonical Problem Walkthroughs

This companion chapter maps each technique in Part III to representative interview problems. Every walkthrough summarises the pattern, highlights pitfalls, and provides annotated Python implementations with complexity analysis.

## Recursion & Backtracking

### Generate Balanced Parentheses
- **Pattern:** depth-first construction with constraints (`open_count ≤ n`, `close_count ≤ open_count`).
- **Pitfalls:** forget to enforce balance constraint before recursing.

```python
def generate_parentheses(n: int) -> list[str]:
    results: list[str] = []

    def backtrack(current: list[str], open_count: int, close_count: int) -> None:
        if len(current) == 2 * n:
            results.append("".join(current))
            return
        if open_count < n:
            current.append("(")
            backtrack(current, open_count + 1, close_count)
            current.pop()
        if close_count < open_count:
            current.append(")")
            backtrack(current, open_count, close_count + 1)
            current.pop()

    backtrack([], 0, 0)
    return results
```

- **Complexity:** `O(C_n)` calls (n-th Catalan number); stack depth `O(n)`.

## Divide and Conquer

### Maximum Subarray (Kadane via Divide & Conquer)
- **Pattern:** split array; answer is max of left, right, or crossing subarray.
- **Pitfalls:** miscompute crossing sum with off-by-one errors.

```python
def max_subarray(values: list[int]) -> int:
    def helper(lo: int, hi: int) -> int:
        if lo == hi:
            return values[lo]
        mid = (lo + hi) // 2
        left = helper(lo, mid)
        right = helper(mid + 1, hi)
        best_left = total = 0
        for i in range(mid, lo - 1, -1):
            total += values[i]
            best_left = max(best_left, total)
        best_right = total = 0
        for i in range(mid + 1, hi + 1):
            total += values[i]
            best_right = max(best_right, total)
        return max(left, right, best_left + best_right)

    return helper(0, len(values) - 1)
```

- **Complexity:** `O(n log n)` time, `O(log n)` stack.

## Sorting & Searching

### Search in Rotated Sorted Array
- **Pattern:** modified binary search; determine which half is sorted each step.
- **Pitfalls:** ignoring duplicates (if allowed) or mis-handling equal pivots.

```python
def search_rotated(nums: list[int], target: int) -> int:
    left, right = 0, len(nums) - 1
    while left <= right:
        mid = (left + right) // 2
        if nums[mid] == target:
            return mid
        if nums[left] <= nums[mid]:  # left half sorted
            if nums[left] <= target < nums[mid]:
                right = mid - 1
            else:
                left = mid + 1
        else:  # right half sorted
            if nums[mid] < target <= nums[right]:
                left = mid + 1
            else:
                right = mid - 1
    return -1
```

- **Complexity:** `O(log n)` time, `O(1)` space.

## Greedy Strategies

### Minimum Number of Coins (Canonical Coin Systems)
- **Pattern:** sort coins descending; take as many as possible of each denomination.
- **Pitfalls:** greedy only optimal for canonical systems (e.g., US coins). Provide counterexample awareness.

```python
def min_coins(amount: int, coins: list[int]) -> int:
    coins.sort(reverse=True)
    count = 0
    for coin in coins:
        take, amount = divmod(amount, coin)
        count += take
    if amount != 0:
        raise ValueError("Greedy failed; coins not canonical")
    return count
```

- **Complexity:** `O(k log k)` for sorting coins; `O(k)` afterwards.

### Merge K Sorted Lists (Greedy + Heap)
- Choose smallest head using min-heap. Complexity `O(n log k)` for `n` total elements and `k` lists.

## Dynamic Programming

### Edit Distance (Levenshtein)
- **Pattern:** 2D DP where `dp[i][j]` = minimum edits to convert `word1[:i]` to `word2[:j]`.
- **Pitfalls:** forgetting to initialise first row/column for insert/delete costs.

```python
def edit_distance(a: str, b: str) -> int:
    m, n = len(a), len(b)
    dp = [[0] * (n + 1) for _ in range(m + 1)]
    for i in range(m + 1):
        dp[i][0] = i
    for j in range(n + 1):
        dp[0][j] = j
    for i in range(1, m + 1):
        for j in range(1, n + 1):
            if a[i - 1] == b[j - 1]:
                dp[i][j] = dp[i - 1][j - 1]
            else:
                dp[i][j] = 1 + min(
                    dp[i - 1][j],     # delete
                    dp[i][j - 1],     # insert
                    dp[i - 1][j - 1], # replace
                )
    return dp[m][n]
```

- **Complexity:** `O(mn)` time and space; optimisable to `O(min(m, n))` space.

## Graph Traversal & Pathfinding

### Word Ladder (BFS on implicit graph)
- **Pattern:** BFS on words, edges connect words differing by one letter.
- **Pitfalls:** generating neighbours inefficiently; precompute wildcard buckets.

```python
from collections import defaultdict, deque

def word_ladder(begin: str, end: str, word_list: list[str]) -> int:
    if end not in word_list:
        return 0
    adjacency = defaultdict(list)
    for word in word_list + [begin]:
        for i in range(len(word)):
            key = word[:i] + "*" + word[i + 1 :]
            adjacency[key].append(word)
    queue = deque([(begin, 1)])
    visited = {begin}
    while queue:
        word, level = queue.popleft()
        if word == end:
            return level
        for i in range(len(word)):
            key = word[:i] + "*" + word[i + 1 :]
            for neighbor in adjacency[key]:
                if neighbor not in visited:
                    visited.add(neighbor)
                    queue.append((neighbor, level + 1))
    return 0
```

- **Complexity:** `O(N * L^2)` pre-processing, `O(N * L)` BFS where `N` = word count, `L` = word length.

### Dijkstra for Network Delay Time
- Use adjacency list + min-heap; track distances and visited set.

## How to use this chapter
- Pair each technique chapter with its canonical walkthroughs for pattern recognition.
- Re-implement problems with variations (e.g., constraints, different data types) to solidify understanding.
- Create flashcards summarising pattern → problem examples for quick review before interviews.

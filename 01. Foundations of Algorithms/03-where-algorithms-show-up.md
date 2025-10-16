# 03 · Where Algorithms Show Up

Knowing the recipe only matters if you recognize when to apply it. This chapter connects algorithm study with the engineering problems and interview prompts you face every day.

## Learning objectives
- Spot common scenarios that reduce to classic algorithmic patterns
- Compare naive and optimized approaches to the same task
- Build intuition for when improving complexity meaningfully changes outcomes

## Real-world touchpoints
- **Product features:** ranking search results, recommending content, deduplicating records.
- **Operational tooling:** scheduling jobs, reconciling metrics, batch-processing data safely.
- **Interviews:** open-ended whiteboard problems, timed coding exercises, system design drills.

Different surfaces, one shared toolkit.

## Case study: maximum pairwise product
The task: given a list of integers, find the two values whose product is maximal. Two Python implementations illustrate why analysts care about complexity:
```python
def pairwise_product_bruteforce(values: list[int]) -> int:
    result = float("-inf")
    for i in range(len(values)):
        for j in range(i + 1, len(values)):
            result = max(result, values[i] * values[j])
    return int(result)


def pairwise_product_linear(values: list[int]) -> int:
    if len(values) < 2:
        raise ValueError("Need at least two numbers")
    second_hi, hi = sorted(values[:2])  # ensure hi is the larger value
    for candidate in values[2:]:
        if candidate >= hi:
            second_hi, hi = hi, candidate
        elif candidate > second_hi:
            second_hi = candidate
    return hi * second_hi
```

`pairwise_product_bruteforce` performs ~`n²/2` comparisons. It is straightforward to reason about, but excruciatingly slow for lists with tens of thousands of elements. `pairwise_product_linear` visits the list once, maintaining only the two largest candidates. On real-world workloads the difference is measured in minutes versus milliseconds.

## Interview checkpoints
- Articulate both the brute-force and improved strategies, even if you only code the faster one.
- Justify why the faster approach is correct: walk through an example and explain the loop invariants.
- Explain trade-offs (time vs. memory) and mention when the brute-force version could still be acceptable.

## Further practice
- Model a feature or bug from your current project as an algorithmic problem. Would a known pattern help?
- Explore the complexity foundations in [04 · Complexity Basics](04-complexity-basics.md) to quantify these trade-offs.

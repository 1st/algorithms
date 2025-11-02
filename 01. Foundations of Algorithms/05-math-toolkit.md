### Code Examples for Permutations and Combinations

Here are small code examples in Python to illustrate the difference between **permutations** and **combinations** using the `itertools` library:

```python
from itertools import permutations, combinations

# Sample list of items
items = ['A', 'B', 'C']

# Permutations: Order matters
print("Permutations (Order Matters):")
for perm in permutations(items, 2):  # Choosing 2 items at a time
    print(perm)

# Combinations: Order does not matter
print("\nCombinations (Order Does Not Matter):")
for comb in combinations(items, 2):  # Choosing 2 items at a time
    print(comb)
```

### Output:
```
Permutations (Order Matters):
('A', 'B')
('A', 'C')
('B', 'A')
('B', 'C')
('C', 'A')
('C', 'B')

Combinations (Order Does Not Matter):
('A', 'B')
('A', 'C')
('B', 'C')
```

### Explanation:
1. **Permutations (`permutations`)**:
   - The order of items is important, so `('A', 'B')` is different from `('B', 'A')`.
   - Result: \( P(3, 2) = 3 \times 2 = 6 \) ordered pairs.

2. **Combinations (`combinations`)**:
   - The order of items does not matter, so `('A', 'B')` is treated the same as `('B', 'A')`.
   - Result: \( C(3, 2) = \frac{3!}{2!(3-2)!} = 3 \) unique pairs.

This demonstrates the key difference: whether or not the order of selection is significant.
# Usage of Algorithms

To learn something - you need to understand why you need this and where you can apply this knowledge.

Below we will provide some examples of code, that solve the same problem differently.
It will show you why one program can solve the same problem much faster than another.

And interesting thing - you don't need think that *"on C my program will work much faster than on python"*,
because if you write ineffective implementation on C - it will work much slower than good implementation
on Python. Just remember this.

## Example of code

The task is to find maximum of `X * Y`, where `X` and `Y` are values from the list `a`.

```python
from random import shuffle

# We have 100'000 integer numbers (from 0 to 100'000).
a = [x for x in range(0, 100000)]
# And shuffle them in a random order.
shuffle(a)

# Solution 1: Very slow.
def solution1(a):
  n = len(a)
  result = 0
  for i in range(0, n):
      for j in range(i+1, n):
          if a[i] * a[j] > result:
              result = a[i] * a[j]
  return result

# Solution 2: Blazing fast.
def solution2(a):
  n = len(a)
  max1, max2 = min(a[0], a[1]), max(a[0], a[1])
  for i in range(2, n):
    if a[i] > max1:
      if max1 > max2:
        max2 = max1
      max1 = a[i]
  return max1 * max2

# Try it. Run this script with solution1 and solution2
# on the same data set.
print(solution2(a))
```

Wow, `solution2` prints result less that in a second, while `solution1` calculate result few minutes.
But they are both print the same correct answer.

*Why one function works in many times faster than another?*
It's because number of computations that computer should do to calculate result is different for each
implementation of the functions.

How to understand if one program is more slow than another?
Read our next article [Program Complexity](02-Complexity.md) to get familiar with it.

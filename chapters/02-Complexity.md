# `02` Program complexity

As you know, computer can do a limited number of computatons per second. The basic operations like
asssign new value or comparison are pretty simple and can be ignored when we calculate a program complexity.
But what is more important - is a loops and function calls.

When we have only one for loop, then we need to produce up to `M` iterations over loop.
When we have second loop after this - it require us up to `M + N` iterations.

But when we have loop inside a loop - it require us up to `M * N` iterations, that is
much more than one simple loop, and even two or 10 loops that go one after another.


## Example of a loops

```python
a = range(50)
b = range(100)

# Solution 1. Two loops, one inside another.
def solution1(a, b):
  result = 0
  for x in a:
    for y in b:
      if x * y > result:
        result = x * y
  return result

# Solution 2. One loop, then second one.
def solution2(a, b):
  m = 0
  n = 0
  for x in a:
    if x > m:
      m = x
  for y in b:
    if y > n:
      n = y
  return m * n
```

Number of lines of code doesn't tell us something about computational complexity of our algorithm.
We need to analyze code to understand which one is more optimized and fast.

As we can see above - it's two versions of a program: each contains two loops, but in a Sample 1
we have loop inside a loop, and in a Sample 2 we have loop after a loop.

**Let's calculate how much simple operations we need to do in each case.**

**Solution 1.** We go over `a` 50 times, and on each iteration we go over all 100 elements in `b`. In total it's `50 * 100` = **5'000 iterations**. Inside each iteration we do simple conditional check and make `x * y` that are not expensive, and we can ignore these lines.

**Solution 2.** We assign few variables, then do one loop with 50 iterations, and then second one - with 100 iterations. In total we have `50 + 100` = **150 iterations**. Inside each loop we do very simple comparison and assign new value to variable. As we can see - we do very similar comparison operation and assignment to variable in each loop.

As a result: for Solution 1 we need to do 5'000 steps, and for Solution 2 - to do 150 steps.
It looks like a number of steps that you need to do, to visit a nearest shop.
What is faster - to do 5'000 steps or only 150 steps to visit a shop?

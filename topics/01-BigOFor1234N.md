# Big O for 1+2+3+4+...+N

Given a code block like this:

```python
for i in range(n):
  for j in range(i+1, n):
    # Do someyhing here.
```

**What is computational complexity of this code *(big O)*?**

## Answer

Answer is `O(n2)`.

## Why?

See on these examples:

```
n = 1
x

n = 2
x x
x

n = 3
x x x
x x
x

n = 4
x x x x
x x x
x x
x

n = 5
x x x x x
x x x x
x x x
x x
x
```

We can find that for `n = 1` we have 1 iteration.
For `n = 2` we have 3 iterations *(1 + 2)*.
For `n = 3` it's 6 iterations *(3 + 3)*.
For `n = 4` it's 10 iterations *(6 + 4)*. And so on.

Looks like computational complexity is `n2 - n`. But it's wrong. For `n = 1` it's zero, that is incorrect.

Correct answer is `O((n2 + n)/2)` -> `O(n2/2 + n/2)` -> `O(n2)`,
because we count only the most valuable part of the expression that grows faster than other and ignore all constants *(in our case it's 1/2)*.

Detailed explanation can be found in the [wikipedia](https://en.wikipedia.org/wiki/1_%2B_2_%2B_3_%2B_4_%2B_⋯).

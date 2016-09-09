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

# Loop 1. Two loops, one inside another.
result = 0
for x in a:
  for y in b:
    if x * y > result:
      result = x * y

# Loop 2. One loop, then second one.
m = 0
n = 0
for x in a:
  if x > m:
    m = x

for y in b:
  if y > n:
    n = y

result = m * n
```

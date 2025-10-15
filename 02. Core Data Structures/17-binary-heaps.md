# 17 · Binary Heaps

Binary heaps support efficient retrieval of the minimum or maximum element while maintaining a partial ordering. They power priority queues, heap sort, and many graph algorithms.

## Learning objectives
- Understand the shape and heap-order properties of binary heaps
- Implement heap operations (push, pop, heapify) and track their complexity
- Use Python’s `heapq` effectively, including common pitfalls
- Recognise when heaps outperform other structures for priority scheduling

## Heap properties
- **Complete binary tree:** nodes fill levels from left to right with no gaps.
- **Heap order:** `min-heap` ensures each node ≤ its children; `max-heap` ensures ≥.
- Represented implicitly using arrays: for index `i`, children are at `2i + 1` and `2i + 2`.

## Operations quick reference

| Operation | Complexity | Notes |
| --- | --- | --- |
| Insert (`push`) | `O(log n)` | Percolate element up |
| Extract min/max (`pop`) | `O(log n)` | Replace root with last element, percolate down |
| Peek (`heap[0]`) | `O(1)` | Access root |
| Build heap (`heapify`) | `O(n)` | Bottom-up heapify |
| Decrease/increase key | `O(log n)` | Adjust value, restore heap |

## Python `heapq` basics

```python
import heapq

data = [5, 1, 9, 3]
heapq.heapify(data)  # O(n); creates min-heap
heapq.heappush(data, 2)
smallest = heapq.heappop(data)
```

- Python’s `heapq` implements a min-heap; to simulate a max-heap, store negative values or wrap elements in custom objects with reversed ordering.
- `heapq.merge` merges sorted iterables lazily (`O(n log k)`).
- To update priorities, push a new pair `(priority, item)` and mark the old entry as invalid (lazy deletion).

## Heapsort (in-place)

```python
def heapsort(iterable: list[int]) -> list[int]:
    heap = list(iterable)
    heapq.heapify(heap)
    return [heapq.heappop(heap) for _ in range(len(heap))]
```

Heapsort runs in `O(n log n)` time, `O(1)` extra space (ignoring output), and is not stable.

## When to use heaps
- Need repeated access to smallest/largest item with interleaved updates (e.g., event scheduling, Dijkstra’s algorithm).
- Maintain top-k elements or streaming medians (combine min/max heaps).
- Implement priority queues where insertion/deletion operations dominate.

## When to look elsewhere
- Random access or search within heap is slow (`O(n)`).
- Need ordering by multiple keys → consider balanced trees.
- Want better constant factors for many decreases/increases → Fibonacci heaps (theoretical) or pairing heaps.

## Interview checkpoints
- Explain array representation and parent/child index math.
- Mention `heapify` complexity (`O(n)`) vs. naive `n log n` inserts.
- Highlight that `heapq` lacks decrease-key operation; use lazy deletion or priority updates.

## Further practice
- Implement a priority queue class wrapping `heapq` with timestamped entries for lazy deletion.
- Solve streaming median (two heaps) and merge k-sorted lists problems.
- Explore heap-based graph algorithms (Prim’s, Dijkstra’s) to reinforce usage.

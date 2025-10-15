# 08 · Bloom Filter Primer

A Bloom filter is a probabilistic set that supports fast membership checks with a tunable false-positive rate. It trades perfect accuracy for significant memory savings.

## Learning objectives
- Understand how Bloom filters represent sets using bit arrays and hash functions
- Calculate false-positive probabilities based on filter size and hash count
- Identify scenarios where Bloom filters outperform exact sets
- Recognise limitations (no deletions without counting, false positives)

## How it works
1. Allocate a bit array of length `m`, initialised to zeros.
2. Choose `k` independent hash functions.
3. To insert element `x`, compute `k` hash positions and set those bits to `1`.
4. To query membership, hash `x` and check if all corresponding bits are `1`.
   - If any bit is `0`, `x` is definitely not in the set.
   - If all bits are `1`, `x` is *probably* in the set (could be false positive).

## False-positive probability
- After inserting `n` elements:
  - Probability a specific bit remains `0`: `(1 - 1/m)^{kn} ≈ e^{-kn/m}`.
  - Probability a bit is `1`: `1 - e^{-kn/m}`.
  - False-positive probability: `(1 - e^{-kn/m})^k`.
- Optimal number of hash functions: `k = (m / n) * ln 2`.
- Choose `m` to achieve target false-positive rate `p`: `m ≈ -(n * ln p) / (ln 2)^2`.

## Python sketch

```python
from hashlib import blake2b

class BloomFilter:
    def __init__(self, capacity: int, error_rate: float):
        from math import ceil, log
        self.size = ceil(-(capacity * log(error_rate)) / (log(2) ** 2))
        self.hash_count = max(1, round((self.size / capacity) * log(2)))
        self.bits = bytearray(self.size // 8 + 1)

    def _hashes(self, item: bytes):
        digest = blake2b(item, digest_size=16).digest()
        for i in range(self.hash_count):
            yield (int.from_bytes(digest, "big") + i * 0x9E3779B1) % self.size

    def add(self, item: str) -> None:
        data = item.encode()
        for idx in self._hashes(data):
            self.bits[idx // 8] |= 1 << (idx % 8)

    def contains(self, item: str) -> bool:
        data = item.encode()
        return all(
            self.bits[idx // 8] & (1 << (idx % 8))
            for idx in self._hashes(data)
        )
```

## When to use Bloom filters
- Need quick membership tests with constrained memory (web caching, CDN routing, databases).
- Filtering probable misses before hitting a slower backend (e.g., blocking known spam senders).
- Tracking large sets where false positives are acceptable but false negatives are not.

## Limitations
- No built-in deletion—setting bits back to `0` introduces false negatives. Counting Bloom filters mitigate this with small counters per bit.
- False positives increase as more elements are inserted; monitor load and resize/filter rebuild when necessary.
- Requires good independent hash functions; correlated hashes raise error rates.

## Interview checkpoints
- Explain the false-positive vs. memory trade-off concisely.
- Derive or at least quote the optimal `k` and `m` formulas for target error rate.
- Mention practical use cases (databases, distributed systems) to demonstrate relevance.

## Further practice
- Implement a counting Bloom filter supporting deletions.
- Compare memory usage between sets and Bloom filters for large key spaces.
- Explore related probabilistic structures: Cuckoo filter, HyperLogLog.

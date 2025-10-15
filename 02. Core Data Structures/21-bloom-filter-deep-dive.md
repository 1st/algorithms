# 21 · Bloom Filter Deep Dive

This chapter builds on the [Bloom Filter Primer](08-bloom-filter-primer.md) to explore tuning strategies, variants, and real-world deployment considerations.

## Learning objectives
- Tune Bloom filter parameters for specific workloads and error budgets
- Understand counting, scalable, and partitioned Bloom filter variants
- Integrate Bloom filters with cache layers and distributed systems
- Evaluate trade-offs between false positives, memory usage, and update patterns

## Parameter tuning
- Target false-positive rate `p`: choose `m` bits and `k` hash functions using:
  - `m ≈ -(n * ln p) / (ln 2)^2`
  - `k = (m / n) * ln 2`
- Precompute tables for common `n` and `p` values to avoid runtime math during interviews.
- When `n` grows beyond expectation, rebuild filter or switch to scalable variants to avoid drifting error rates.

### Example sizing table (n = 1e6)

| `p` (false positive) | `m` (bits) | `m` (MB) | `k` |
| --- | --- | --- | --- |
| 0.01 | ~9.6e6 | 1.2 MB | 7 |
| 0.001 | ~14.4e6 | 1.8 MB | 10 |
| 0.0001 | ~19.1e6 | 2.4 MB | 13 |

## Implementation considerations
- Use independent hash functions by seeding a base hash (`murmur`, `blake2`) and deriving additional hashes with double hashing: `h_i(x) = h1(x) + i * h2(x)`.
- Store bits in packed arrays (`bytearray`, `bitarray`, `numpy.bool_`) to minimise memory.
- Consider thread safety: operations are idempotent but not atomic; use locks or atomic bit operations if concurrent updates matter.

## Variants
- **Counting Bloom filter:** replace bit array with small counters (4–8 bits). Supports deletions; increments/decrements counters on insert/delete.
- **Scalable Bloom filter:** maintain series of Bloom filters with increasing size when load factor exceeds threshold. Keeps false-positive rate bounded.
- **Partitioned Bloom filter:** divide bit array into `k` partitions, one per hash function—improves cache locality.
- **Compressed Bloom filter:** reduce memory for disk or network transmission at the cost of higher false positives.

## Integration patterns
- **Caches:** store Bloom filter alongside cache to avoid backend lookups for missing keys (CDNs, key-value stores).
- **Databases:** use Bloom filters to skip disk reads in LSM trees (Cassandra, HBase); each SSTable has a Bloom filter.
- **Security:** maintain sets of revoked credentials or malicious IPs; false positives trigger deeper inspection.

## Monitoring and maintenance
- Track estimated fill ratio: `(1 - e^{-kn/m})`. Rising above design target signals the need for rebuild.
- Instrument false positives vs. actual misses in staging to calibrate parameters.
- Provide rolling rebuilds when data sets evolve; maintain two filters during migration to avoid spikes.

## Interview checkpoints
- Mention advanced variants when asked “how to handle deletions?” or “what if the dataset grows?”
- Connect Bloom filters to real systems (databases, caches) to demonstrate practical awareness.
- Be ready to discuss hash function choices and independence assumptions.

## Further practice
- Implement a counting Bloom filter and measure memory overhead.
- Build a scalable Bloom filter that appends new layers when load exceeds a threshold.
- Evaluate false-positive rates empirically with random test data to validate calculations.

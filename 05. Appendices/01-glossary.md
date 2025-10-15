# 01 · Glossary of Terms and Notation

Use this glossary to refresh key vocabulary and symbols used throughout the book. Entries are grouped alphabetically for quick lookup.

## A
- **Adjacency list / matrix:** Data structures representing graphs. List stores per-vertex neighbour lists; matrix stores `|V|×|V|` boolean or weighted entries.
- **Amortised analysis:** Averaging cost of operations over a sequence (e.g., dynamic array `append`).
- **Algorithm:** Step-by-step procedure to solve a problem; focus of this book.

## B
- **Balanced tree:** Binary tree maintaining `O(log n)` height via rotations (AVL, Red-Black).
- **Big-O notation (`O`):** Upper bound on growth rate; ignores constant factors.
- **Big-Ω (`Ω`), Big-Θ (`Θ`):** Lower bound and tight bound counterparts to Big-O.
- **Bloom filter:** Probabilistic set structure allowing false positives but not false negatives.
- **Breadth-first search (BFS):** Graph traversal exploring neighbours level by level.

## C
- **Complexity:** Measure of time or space usage as input size grows.
- **Combinatorics:** Counting methods useful for DP and probability questions (permutations, combinations).
- **Connected component:** Set of vertices reachable from each other in a graph.
- **Convex hull trick:** Optimisation for DP with linear recurrences.

## D
- **Depth-first search (DFS):** Traversal diving down paths before backtracking.
- **Disjoint set union (DSU):** Union-Find structure tracking connectivity.
- **Dynamic programming (DP):** Optimisation by combining overlapping subproblems.

## E
- **Edge (graph):** Connection between two vertices; may be directed or weighted.
- **Expected value:** Average outcome used in probability analysis (e.g., hash collisions).
- **Exponential growth:** Complexity class `O(c^n)`; typically infeasible for large `n`.

## F
- **Fibonacci heap:** Heap with low amortised `decrease-key`, used in theoretical bounds.
- **Flow (network):** Amount passing through edges subject to capacities; relevant for max-flow problems.

## G
- **Greedy algorithm:** Strategy making locally optimal choices hoping for global optimum.
- **Graph:** Set of vertices and edges modelling relationships.

## H
- **Hash function:** Maps keys to integers; used in hash tables/sets.
- **Heap:** Tree-based priority queue supporting fast min/max retrieval.
- **Heuristic:** Approximation guide in algorithms like A*, not guaranteed optimal.

## I
- **Invariant:** Property maintained throughout algorithm execution; crucial for proofs.
- **Interval scheduling:** Greedy problem selecting maximum compatible intervals.
- **Inverse Ackermann function (`α(n)`):** Extremely slow-growing function; DSU complexity.

## J
- **Jump list / Skip list:** Probabilistic data structure offering expected `O(log n)` search.

## K
- **Kruskal’s algorithm:** Greedy MST algorithm using sorted edges and DSU.
- **Knapsack problem:** DP optimisation packing items subject to weight constraints.

## L
- **Level-order traversal:** BFS of a tree grouping nodes by depth.
- **LRU cache:** Eviction policy removing least recently used entries.
- **Logarithm (`log_b n`):** Inverse of exponentiation; key to complexity analysis.

## M
- **Master Theorem:** Tool for solving divide-and-conquer recurrences.
- **Memoisation:** Caching results of recursive calls (top-down DP).
- **Minimum spanning tree (MST):** Subset of edges connecting all vertices with minimum total weight.

## N
- **Node:** Vertex in trees or graphs; also element in linked structures.
- **NP-complete:** Class of problems believed hard to solve optimally but easy to verify solutions.

## O
- **Optimal substructure:** Overlapping subproblems enabling DP or greedy approaches.
- **Order statistic:** k-th smallest/largest element; supported by augmented trees.

## P
- **Path compression:** DSU optimisation flattening tree height.
- **Priority queue:** Abstract data type retrieving highest-priority element quickly (often heap-backed).
- **Probability distribution:** Function assigning likelihoods; used in randomised algorithms.

## Q
- **Queue:** FIFO structure; `deque` for `O(1)` enqueues/dequeues.

## R
- **Recursion:** Function calling itself with smaller inputs.
- **Red-Black tree:** Balanced BST enforcing colour properties.
- **Rolling hash:** Hashing technique reusing computation for sliding windows.

## S
- **Segment tree:** Tree supporting range queries and updates.
- **Space complexity:** Memory usage as a function of input size.
- **Stable sort:** Sorting algorithm preserving relative order of equal elements.

## T
- **Topological sort:** Linear ordering of DAG vertices respecting edge direction.
- **Trie:** Prefix tree storing strings character by character.
- **Time complexity:** Running time growth with input size.

## U
- **Union operation:** DSU method merging two sets.
- **Upper bound:** Worst-case behaviour; Big-O expresses this.

## V
- **Vertex:** Node in a graph.
- **Visited set:** Structure tracking explored nodes in traversal.

## W
- **Weighted graph:** Graph whose edges carry costs or weights.
- **Window (sliding):** Technique maintaining subarray using two pointers.

## X
- **XOR (exclusive OR):** Bitwise operation toggling bits; used in parity problems.

## Y
- **Yield (Python):** Produces value from generator; useful for lazy traversals.

## Z
- **Zero-based indexing:** Arrays start at index 0 (Python, C); always clarify in interviews.

Add to this glossary as the book grows to keep terminology consistent.

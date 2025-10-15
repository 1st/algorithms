# 08 · Review Checklists and Quick Guides

Use this chapter as a rapid refresher before interviews. Each technique gets a pre-flight checklist, a high-level decision guide, and references to visual mnemonics or diagrams you can sketch on a whiteboard.

## Technique snapshot table

```
Technique          | Core Questions                                 | Go-to Tools
-------------------+-------------------------------------------------+-----------------------------
Recursion/Backtracking | Is there a natural branching decision tree?   | Call-stack diagrams, pruning
Divide & Conquer   | Can we split evenly and merge efficiently?      | Recursion tree, Master theorem
Sorting & Searching| Does ordering unlock an easy invariant?         | Two pointers, binary search variants
Greedy             | Is there a local choice that stays globally optimal? | Exchange argument sketch
Dynamic Programming| Do subproblems overlap with optimal substructure?| State grid, dependency arrows
Graph Pathfinding  | What graph traits matter (weights, direction)?  | BFS/DFS layers, frontier expansion
```

## Recursion & Backtracking checklist
- [ ] Confirm base cases cover all termination paths.
- [ ] Track recursion depth vs. stack limits; convert to iterative if needed.
- [ ] Define state variables (path, choices, visited) and how to undo them.
- [ ] Add pruning condition—explain to interviewer why it is safe.
- [ ] Sketch a small recursion tree (2–3 levels) to communicate flow.

**Diagram prompt:** draw a branching tree with green ticks for explored nodes and red crosses for pruned branches.

## Divide and Conquer checklist
- [ ] State recurrence `T(n)` explicitly and identify `a`, `b`, and `f(n)`.
- [ ] Specify combine step complexity and required temporary space.
- [ ] Mention worst vs. average case (e.g., quicksort pivot choices).
- [ ] Prepare a recursion-tree or Master Theorem justification.
- [ ] Note parallelisation opportunities (subcalls independent?).

**Diagram prompt:** recursion tree showing size halves each level; annotate per-level cost.

## Sorting & Searching checklist
- [ ] Clarify stability, in-place requirement, and data size constraints.
- [ ] If sorting first, justify trade-off (`O(n log n)` preprocessing vs. linear scans).
- [ ] For binary search, define invariant (e.g., `left` always ≤ target index).
- [ ] Mention library sort fallback when constraints permit.
- [ ] Prepare quick table of algorithm properties (merge, quick, heap) to reference.

**Diagram prompt:** timeline of sorted array with two-pointer arrows moving inward/outward.

## Greedy checklist
- [ ] Define scoring heuristic and ordering (sort key or priority queue).
- [ ] State feasibility condition checked at each step.
- [ ] Present correctness argument (exchange argument or matroid intuition).
- [ ] Highlight counterexample if heuristic fails—shows understanding of limits.
- [ ] Map data structure choice (heap, DSU, sort) to operations cost.

**Diagram prompt:** timeline showing greedy picks with justification notes.

## Dynamic Programming checklist
- [ ] Write down state definition and meaning of indices.
- [ ] Derive recurrence before coding; specify base cases.
- [ ] Discuss implementation choice (top-down vs. bottom-up) and memory footprint.
- [ ] Identify transition order (row-wise, column-wise, diagonals).
- [ ] Consider optimisations (rolling arrays, bitmask compression, monotonic queues).

**Diagram prompt:** grid with arrows showing dependency edges; highlight topological order of fills.

## Graph traversal & pathfinding checklist
- [ ] Classify graph: directed? weighted? negative edges? cyclic?
- [ ] Choose traversal/algorithm (BFS, DFS, Dijkstra, Bellman-Ford, A*, topological DP).
- [ ] Describe visited tracking strategy and prevent reprocessing.
- [ ] If shortest path, indicate how you reconstruct path (parent pointers).
- [ ] Mention complexity in `|V|` and `|E|` terms; watch sparse vs. dense implications.

**Diagram prompt:** node layers for BFS, with frontier queue displayed; note distance increments.

## Quick-reference flow

```
Need optimal solution?
└─> Subproblems overlap? ── Yes ──► Dynamic Programming
                     │
                     No
                     │
 Balanced divide step? ──► Divide & Conquer
                     │
 Greedy choice provable? ──► Greedy
                     │
 Natural recursion tree? ──► Recursion/Backtracking
                     │
 Graph structure? ──► Graph Traversal/Pathfinding
```

Sketch this flowchart to orient yourself and articulate reasoning during interviews.

## Preparation tips
- Keep a blank sheet to sketch diagrams mentioned above; draw while explaining.
- Use the canonical walkthroughs (Chapter 07) as daily drills—time yourself solving each.
- Record complexity summaries (time/space) on flashcards; review before sessions.
- Practise explaining trade-offs aloud; clarity often matters more than raw speed.

Carry this checklist into your final review session, and cross off items as you rehearse each technique.

# Solution to Part 1

Do nothing, it's still a Minimum Spanning Tree (MST).


# Solution to Part 2

Do nothing, it's still a Minimum Spanning Tree (MST).


# Solution to Part 3

Main idea: Removing `e` creates 2 subtrees. Search all `m` edges for smallest edge that reconnects the 2 subtrees.

1. Removing `e` results in 2 subtrees T<sub>u</sub> and T<sub>v</sub> (that are probably not connected. They are only connected if u or v was a leaf in T).
1. Find out which vertices are in T<sub>u</sub> and which are in T<sub>v</sub>. Can do this by running [BFS](https://github.com/RodneyShag/Interview_solutions/blob/master/Solutions/Cracking%20the%20Coding%20Interview/Breadth-First%20Search.md) from `u`, and also from `v` (if the original BFS didn't cover all the nodes).
1. Loop through all edges and pick the one with lowest weight that has 1 end in T<sub>u</sub> and another in T<sub>v</sub>. This will be the new edge. (could possibly be same edge as original edge `e`).

#### Time/Space Complexity

- Time Complexity: `O(n + m)`. O(n) is for BFS on a tree, and O(m) is for looping through edges.
- Space Complexity: `O(1)` since we're not saving anything.


# Solution to Part 4

1. Let e = (u, v). Add e to T, which will create a unique cycle.
1. Find this cycle by doing [BFS](https://github.com/RodneyShag/Interview_solutions/blob/master/Solutions/Cracking%20the%20Coding%20Interview/Breadth-First%20Search.md) on our updated tree, ignoring weights.
1. Loop through edges in the cycle and remove the maximum weight edge.

#### Time/Space Complexity

- Time Complexity: `O(n)` for BFS on a tree with 1 added edge. This is because our number of edges is bounded by number of nodes.
- Space Complexity: `O(1)` since we're not saving anything.

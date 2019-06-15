# Solution

### Algorithm

1. Let `G' = (V, E - E')`
1. Create `h + 1` copies of `G'` as G<sub>0</sub>, ... G<sub>h</sub>
1. if `(u, v)` is a risky edge in `G`, include a _directed_ edge from `u` in G<sub>i</sub> to `v` in G<sub>i+1</sub>
1. Run [Dijkstra's Algorithm](https://github.com/RodneyShag/Interview_solutions/blob/master/Solutions/Custom/Dijkstra%27s%20Algorithm.md) from start vertex `s`. Now dijstraDistance(s, v<sub>i</sub>) represents shortest path from `s` to `v` in original graph `G` using exactly `i` risky edges.
1. To calculate our solution (the distance from `s` to `v` in original graph `G` using at most `h` risky edges), we calculate: minimum<sub>0<=i<=h</sub> { dijkstraDistance(s, v<sub>i</sub>) }.

### Time/Space Complexity

- Time Complexity: Dijkstra's algorithm is generally O(m + n log n), but since we have `mh` edges and `nh` nodes, our complexity becomes `O(mh + nh log (nh))`
- Space Complexity: `O(mh + nh)` to create `G'`

# Follow-up Solution

Use the same algorithm as above, but instead of creating `h + 1` copies of `G'`, extend it to create h<sub>i</sub>h<sub>j</sub> + 1 copies of `G'`, where the h<sub>i</sub>h<sub>j</sub> copy represents having traversed `i` blue edges and `j` red edges.

### Time/Space Complexity

Same as above, but replace each `h` with h<sub>i</sub>h<sub>j</sub>

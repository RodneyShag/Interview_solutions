### Algorithm

1. Notice it's a __directed__ graph with __weighted__ edges.
1. Run [Dijkstra's Algorithm](https://github.com/RodneyShag/Interview_solutions/blob/master/Solutions/Custom/Dijkstra%27s%20Algorithm.md) from node `s` to give us the shortest path to every other node. If the edges weren't weighted, we could simply use [BFS](https://github.com/RodneyShag/Interview_solutions/blob/master/Solutions/Cracking%20the%20Coding%20Interview/Breadth-First%20Search.md) instead.
1. Let
    - `N` be the set of vertices in our graph.
    - `n` be 1 node in `N`.
    - `dijkstraDistance(s, n)` be the shortest distance from node `s` to `n` without using the edge between them (since that edge is directed from `n` to `s`)
    - `lengthOfDirectedEdge(n, s)` be the length of the directed edge from node `n` to node `s`. If such an edge doesn't exist, let this function return infinity.
1. Shortest cycle is: For every `n` in `N`, the minimum value of `dijkstraDistance(s, n) + lengthOfDirectedEdge(n, s)`. Notice this formula should only be used if an edge from `n` to `s` exists.

### Time/Space Complexity

- Time Complexity: `O(m + n log n)` to run Dijkstra's algorithm.
- Space Complexity: `O(n)` due to Dijkstra's algorithm

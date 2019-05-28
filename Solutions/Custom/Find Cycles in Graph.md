### Algorithm

1. Find the connected components of G. This can be done by running BFS on each node in Graph until all nodes are visited.
1. Notice trees have exactly 1 less edge than they have vertices, so for each connected component, if |E| = |V| then it has 1 cycle, and if |E| = |V| + 1 then it has 2 cycles
1. To _find_ the cycle in a component that has one
    1. Run BFS or DFS from any vertex and get a (spanning) tree T.
    1. pick an edge (u, v) that's not in the tree.
    1. Run BFS or DFS from vertex u in Tree T to get a simple path from u to v (Recall (u, v) is not an edge in T).
    1. Add (u, v) to this simple path to get a cycle.
1. If there are 2 cycles, then there are 2 edges like (u, v) so we do the above algorithm twice.

### Time/Space Complexity

- Time Complexity: O(n + m), as that's the runtime of BFS/DFS
- Space Complexity: O(1), assuming graph nodes can be marked visited.

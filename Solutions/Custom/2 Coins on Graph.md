### Algorithm

Following the hint, we form a graph. But what graph? In many problems involving games, or in problems where the goal is to find a sequence of operations to effect some change, we can use a _state space graph_: This is a graph where the vertices represent states, or snapshots, of the domain of interest, and edges represent actions that move the system from one state to another.

In this case, a state of the system can be represented by the original graph together with the location of the two coins. If we know the graph, we can simply represent a state by a pair of vertices (u, v) indicating that coins 1 and 2 are on vertices u and v respectively.

Let the original input graph be G = (V, E). We define the graph G' = (V', E') as follows:

- V' = V x V
- E' = { ((u<sub>1</sub>, v<sub>1</sub>),(u<sub>2</sub>, v<sub>2</sub>)) | (u<sub>1</sub>, u<sub>2</sub>) and (v<sub>1</sub>, v<sub>2</sub>) are both in E }.

The edges represent the fact that if the coins were on u1 and v1 respectively, and there was an edge from u1 to u2 and from v1 to v2, then the coins could each move to their respective vertices, resulting with the coins on vertices u2 and v2.

The problem now reduces to that of determining whether from the initial vertex (s, t) in G', it is possible to reach a vertex of the form (u, u). This can be done via any linear-time search technique in G' to find those vertices connected to (s, t).

### Time/Space Complexity

We must be careful about stating the running time, since it is not in fact linear. The original graph G has n vertices and m edges. But the new graph has |V'| = n<sup>2</sup> vertices (one for each pair (u, v)), and m<sup>2</sup> edges (if (u<sub>1</sub>, u<sub>2</sub>) and (v<sub>1</sub>, v<sub>2</sub>) are each edges of E, then there is a corresponding edge ((u<sub>1</sub>, v<sub>1</sub>), (u<sub>2</sub>, v<sub>2</sub>)) of E').

The running time depends on the time to build this new graph, which can be done in O(n<sup>2</sup> + m<sup>2</sup>) time, plus the time to search it, which is linear in the size of the new graph, hence another O(n<sup>2</sup> + m<sup>2</sup>).

Thus, the running time of the algorithm is O(n<sup>2</sup> + m<sup>2</sup>).

A simple example of an unsolvable instance is a two-node graph connected by a single edge, with
the coins starting on different nodes.

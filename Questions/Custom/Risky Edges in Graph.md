### Question

- Let
    - `G = (V, E)` be a directed graph with `V` vertices and `E` edges.
    - `E'` be a subset of `E`, where each edge in `E'` is considered _risky_.
    - `s` be the start node.
    - `v` be a vertex in `V`.
    - `h` be an integer representing the maximum number of risky edges you're allowed to use when finding the shortest path from `s` to every vertex `v`.

Find the shortest path from `s` to every vertex `v` using at most `h` risky edges.

### Follow-up Question

Suppose there are 2 different types of risky edges: blue and red.

Solve the same problem as above using at most h<sub>1</sub> risky blue edges and at most h<sub>2</sub> risky red edges.

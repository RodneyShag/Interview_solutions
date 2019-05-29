### Question

Suppose we are given both an undirected graph `G` with weighted edges and a minimum spanning tree `T` of `G`.

In all cases, the input to your algorithm is the edge `e` and its new weight.

Your algorithms should modify `T` so that it is still a minimum spanning tree.

Of course, we could just recompute the minimum spanning tree from scratch in O(m n log n) time, but you can do better.

- Describe an efficient algorithm to update the minimum spanning tree when
    1. the weight of one edge `e` in `T` is decreased.
    2. the weight of one edge `e` not in `T` is increased.
    3. the weight of one edge `e` in `T` is increased.
    4. the weight of one edge `e` not in `T` is decreased.

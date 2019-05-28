### Algorithm

We will create a bipartite graph with 2n vertices. Each vertex represents an event. For 1 ≤ i ≤ n, let vertex B<sub>i</sub> represent the birth of P<sub>i</sub>, and let vertex D<sub>i</sub> represent the death of P<sub>i</sub>. A directed edge from an arbitrary vertex u to an arbitrary vertex v indicates that the event represented by vertex u precedes the event represented by vertex v.

We will draw an initial n edges: For 1 ≤ i ≤ n, we will draw a directed edge from B<sub>i</sub> to D<sub>i</sub>. This represents the necessity that a person must be born before that person can die (and we are told that everyone is deceased).

Now we will loop through the facts. Each fact can be represented by 1 or 2 directed edges.

- Each fact of the form "For some i and j, person P<sub>i</sub> died before person P<sub>j</sub> was born," can be represented as a directed edge from D<sub>i</sub> to B<sub>j</sub>.
- Each fact of the form "For some i and j, the life spans of P<sub>i</sub> and P<sub>j</sub> overlapped at least partially," can be represented by 2 directed edges. One directed edge will be from B<sub>i</sub> to D<sub>j</sub>, and another directed edge will be from B<sub>j</sub> to D<sub>i</sub>

Lemma: A directed graph has a cycle if and only if it has a "back-edge".

To determine if the facts are consistent, all we have to do is determine whether our graph (lets call it G) has a cycle. For a directed connected graph, we could simply run [DFS](https://github.com/RodneyShag/Interview_solutions/blob/master/Solutions/Cracking%20the%20Coding%20Interview/Depth-First%20Search.md) on the graph. Using our lemma above, if there are any back-edges, then the graph has a cycle. However, our graph G is not necessarily connected, and we want DFS to visit all 2n nodes. To achieve this, we will have to run `DFSall` (which is basically just running DFS from every node) to ensure all 2n nodes are visited. If a back-edge exists, then G has a cycle. If a back-edge does not exist, then G does not have a cycle.

Notice that if G has a cycle, then each vertex that represents an event must precede another event in the cycle. But this is impossible. Each vertex/event in the cycle has an incoming arrow, so there is no vertex/event that could have possibly occurred first. So we can conclude that the facts are inconsistent.

If it is the case that G does not have a cycle, then G is a DAG. We can [topological sort](https://github.com/RodneyShag/Interview_solutions/blob/master/Solutions/Cracking%20the%20Coding%20Interview/Build%20Order.md) the DAG to provide an ordering that does not have any inconsistencies. This ordering will be consistent with the presented facts.

### Time/Space Complexity

- Time Complexity: O(n + m) due to DFS.
- Space Complexity: O(n + m) since we create a graph.

### Solution

- Bidirectional search is using 2 simultaneous BFS searches to find the distance between 2 __nodes__. These searches can optionally be done in parallel on 2 different threads.

### Time Complexity

- For BFS, if `d` is the distance between the 2 nodes, and `b` is the branching factor, 1 way to represent the runtime is `O(b^d)`.
- For Bidirectional search, the runtime is `O(b^(d/2))` since each search only has to search halfway before meeting the other search.

![Bidirectional Search](./../images/BidirectionalSearch.png)

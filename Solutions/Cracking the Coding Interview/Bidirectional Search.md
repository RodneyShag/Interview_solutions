### Solution

Bidirectional search is using 2 simultaneous BFS searches to find the distance between 2 __nodes__.

### Time Complexity

For BFS, if `d` is the distance between the 2 nodes, and `b` is the branching factor, 1 way to represent the runtime is O(b<sup>d</sup>).

![Bidirectional Search](./../images/BidirectionalSearch.png)

For Bidirectional search, the runtime is O(b<sup>(d/2)</sup>) + O(b<sup>(d/2)</sup>) = O(2*b<sup>(d/2)</sup>) = O(b<sup>(d/2)</sup>) since each search only has to search halfway before meeting the other search.

### Solution

```java
@Getter
class GraphNode {
    private int data;
    private boolean visited; // needed for BFS, DFS
    private List<GraphNode> neighbors; // can alternatively use a HashSet (and give nodes unique IDs)

    public GraphNode(int data) {
        this.data = data;
        visited = false;
        neighbors = new ArrayList();
    }

    public void visit() {
        visited = true;
    }

    public void addNeighbor(GraphNode neighbor) {
        neighbors.add(neighbor);
        neighbor.neighbors.add(this);
    }

    public void addDirectedNeighbor(GraphNode neighbor) {
        neighbors.add(neighbor);
    }
}
```

### Time/Space Complexity

- Time Complexity: O(1) for GraphNode(), visit(), addNeighbor(), addDirectedNeighbor().
- Space Complexity: O(1) for GraphNode(), visit(), addNeighbor(), addDirectedNeighbor(). Each GraphNode requires O(1) storage for itself, and an additional O(1) storage for each neighbor in `neighbors`.

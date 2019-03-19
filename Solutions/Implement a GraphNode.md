### Solution

```java
@Getter
class GraphNode {
    private int data;
    private boolean visited; // needed for BFS, DFS
    private ArrayList<GraphNode> neighbors; // can alternatively use a HashSet (and give nodes unique IDs)

    /* Constructor */
    public GraphNode(int data) {
        this.data = data;
        visited = false;
        neighbors = new ArrayList<>();
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

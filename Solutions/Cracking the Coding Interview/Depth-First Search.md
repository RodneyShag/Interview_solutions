### Provided Code

- [GraphNode](https://github.com/RodneyShag/Interview_solutions/blob/master/Solutions/Implement%20a%20GraphNode.md)

### Solution

```java
DFS(GraphNode node, int data) {
    if (node == null) {
        return;
    }

    if (node.data == data) {
        System.out.println("DFS found the GraphNode with desired data: " + node.data);
        return; // although we return, the DFS search keeps going in this implementation
    }

    for (GraphNode neighbor : node.getNeighbors()) {
        if (!neighbor.visited) {
            neighbor.visit(); // crucial step
            DFS(neighbor, data);
        }
    }
}
```

### Time Complexity

There are 2 ways to represent the time complexity
- `O(n + m)` on a graph with `n` nodes and `m` edges, since we may have to search the entire graph to find what we're looking for.
- `O(b ^ m)` for a graph with branching factor `b` and maximum depth `m`

### Alternate Solution

The above solution is recursive. Can alternatively code DFS iteratively like in our [BFS solution](https://github.com/RodneyShag/Interview_solutions/blob/master/Solutions/Breadth-First%20Search.md), by using a Stack instead of a Queue.

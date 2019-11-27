### Algorithm

Run Breadth-First Search (BFS) from start node and see if we arrive at end node

### Solution

We are provided 2 [GraphNode](https://github.com/RodneyShag/Interview_solutions/blob/master/Solutions/Cracking%20the%20Coding%20Interview/Implement%20a%20GraphNode.md)s.

```java
boolean routeExists(GraphNode start, GraphNode end) {
    if (start == end) {
        return true;
    }

    Deque<GraphNode> deque = new ArrayDeque(); // use deque as a queue
    start.visit();
    deque.add(start);

    while (!deque.isEmpty()) {
        GraphNode curr = deque.remove();
        if (curr == end) {
            return true;
        }
        for (GraphNode neighbor : curr.getNeighbors()) {
            if (!neighbor.visited) {
                neighbor.visit();
                deque.add(neighbor);
            }
        }
    }
    return false;
}
```

Time/Space Complexity same as [BFS](https://github.com/RodneyShag/Interview_solutions/blob/master/Solutions/Cracking%20the%20Coding%20Interview/Breadth-First%20Search.md)

### Improvement

If this was an _undirected_ graph, we could do Bidirectional Search to improve runtime.

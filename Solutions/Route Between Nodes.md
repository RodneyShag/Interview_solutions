#### Algorithm

- Run Breadth-First Search (BFS) from start node and see if we arrive at end node

#### Solution

We are provided 2  [TreeNode](https://github.com/RodneyShag/Interview_solutions/blob/master/Solutions/Implement%20a%20TreeNode.md)s.

```java
boolean routeExists(GraphNode start, GraphNode end) {
    if (start == end) {
        return true;
    }

    ArrayDeque<GraphNode> deque = new ArrayDeque<>(); // use deque as a queue
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

#### Improvement

- Do bi-directional BFS to improve runtime

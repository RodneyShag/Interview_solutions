### Provided Code

[GraphNode](https://github.com/RodneyShag/Interview_solutions/blob/master/Solutions/Cracking%20the%20Coding%20Interview/Implement%20a%20GraphNode.md)

### Tips

1. Use a Queue (or `ArrayDeque` as a Queue)
1. .visit() a node before we add it to deque (to avoid duplicates on deque)

### Solution

```java
void BFS(GraphNode node, int data) {
    if (node == null) {
        return;
    }

    Deque<GraphNode> deque = new ArrayDeque<>(); // use deque as a queue
    node.visit();
    deque.add(node);

    while (!deque.isEmpty()) {
        GraphNode curr = deque.removeFirst();

        if (curr.data == data) {
            System.out.println("BFS found the GraphNode with desired data: " + curr.data);
            return;
        }

        for (GraphNode neighbor : curr.getNeighbors()) {
            if (!neighbor.visited) {
                neighbor.visit();
                deque.addLast(neighbor);
            }
        }
    }
}
```

### Time Complexity

There are 2 ways to represent the time complexity

- O(n + m) On a graph with `n` nodes and `m` edges, since we may have to search the entire graph to find what we're looking for.
- O(b<sup>d</sup>) for a graph with branching factor `b` and location of data at depth `d`

### Space Complexity

O(n) due to `deque` to store our nodes.

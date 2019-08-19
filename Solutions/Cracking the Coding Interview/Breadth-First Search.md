### Tips

1. Use a Queue (or `Deque` as a Queue)
1. "mark" a node before we add it to `Deque` (to avoid duplicates on `Deque`)

### Solution

```java
class GraphNode {
    int data;
    boolean marked;
    List<GraphNode> neighbors;
}
```

```java
void BFS(GraphNode root, int data) {
    if (node == null) {
        return;
    }

    Deque<GraphNode> deque = new ArrayDeque<>(); // use deque as a queue
    root.marked = true;
    deque.add(root);

    while (!deque.isEmpty()) {
        GraphNode curr = deque.removeFirst();

        if (curr.data == data) {
            System.out.println("Success");
            return;
        }

        for (GraphNode neighbor : curr.getNeighbors()) {
            if (neighbor.marked == false) {
                neighbor.marked = true;
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

`O(n)` to store nodes in our `deque`.

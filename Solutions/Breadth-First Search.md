#### Provided Code

- [GraphNode](https://github.com/RodneyShag/Interview_solutions/blob/master/Solutions/Implement%20a%20GraphNode.md)

#### Tips

1. Use a Queue (or `ArrayDeque` as a Queue)
1. .visit() a node before we add it to deque (to avoid duplicates on deque)

#### Solution

```java
void BFS(GraphNode node, int data) {
    if (node == null) {
        return;
    }

    ArrayDeque<GraphNode> deque = new ArrayDeque<>(); // use deque as a queue
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
                neighbor.visit(); // visit node BEFORE adding it to deque instead of when we take it off (to avoid duplicates on queue)
                deque.addLast(neighbor);
            }
        }
    }
}
```

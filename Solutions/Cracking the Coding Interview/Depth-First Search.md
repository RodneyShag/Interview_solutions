### Solution

```java
class GraphNode {
    int data;
    boolean marked;
    List<GraphNode> neighbors;
}
```

```java
void DFS(GraphNode n, int data) {
    if (n == null) {
        return;
    }

    if (n.data == data) {
        System.out.println("Success");
        return; // although we return, the DFS search keeps going in this implementation
    }

    for (GraphNode neighbor : n.neighbors) {
        if (neighbor.marked == false) {
            neighbor.marked = true;
            DFS(neighbor, data);
        }
    }
}
```

### Time Complexity

There are 2 ways to represent the time complexity
- O(n + m) on a graph with `n` nodes and `m` edges, since we may have to search the entire graph to find what we're looking for.
- O(b<sup>m</sup>) for a graph with branching factor `b` and maximum depth `m`

### Space Complexity

O(n) since that's the maximum number of recursive calls existing at the same time in the call stack.

### Alternate Solution

The above solution is recursive. Can alternatively code DFS iteratively by using our [BFS solution](https://github.com/RodneyShag/Interview_solutions/blob/master/Solutions/Cracking%20the%20Coding%20Interview/Breadth-First%20Search.md) and replacing the `Queue` there with a `Stack`.

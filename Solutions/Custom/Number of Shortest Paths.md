### Sample Graph we will use

Letters are Nodes.

```
 a ----- b ----- c ----- d ----- f
         |       |               |
         |       |               |
         |       |               |
         e ----- g ------------- h
```

### Algorithm

- Use a modified version of [BFS](https://github.com/RodneyShag/Interview_solutions/blob/master/Solutions/Cracking%20the%20Coding%20Interview/Breadth-First%20Search.md)
- Each `GraphNode` will keep track of 2 additional pieces of information
    - `level` will represent how for we are from the source node. Any node that has `level = Integer.MIN_VALUE` has not been visited yet.
    - `numPaths` will represent the number of shortest paths from source node to current node.

### Code

```java
class GraphNode { // public variables for simplicity
    char data;
    List<GraphNode> neighbors = new ArrayList<>();
    int level = Integer.MIN_VALUE;
    int numPaths = 0;

    public GraphNode(char data) {
        this.data = data;
    }

    public void addNeighbor(GraphNode neighbor) {
        addDirectedNeighbor(neighbor);
        neighbor.addDirectedNeighbor(this);
    }

    public void addDirectedNeighbor(GraphNode neighbor) {
        neighbors.add(neighbor);
    }
}
```

```java
import java.util.*;

public class NumberOfShortestPaths {
    public static void main(String[] args) {
        // Create Graph
        GraphNode a = new GraphNode('a');
        GraphNode b = new GraphNode('b');
        GraphNode c = new GraphNode('c');
        GraphNode d = new GraphNode('d');
        GraphNode e = new GraphNode('e');
        GraphNode f = new GraphNode('f');
        GraphNode g = new GraphNode('g');
        GraphNode h = new GraphNode('h');
        a.addNeighbor(b);
        b.addNeighbor(c);
        c.addNeighbor(d);
        d.addNeighbor(f);
        b.addNeighbor(e);
        e.addNeighbor(g);
        c.addNeighbor(g);
        g.addNeighbor(h);
        h.addNeighbor(f);

        Queue<GraphNode> queue = new LinkedList<>();
        a.level = 0;
        a.numPaths = 1;
        queue.add(a);

        while (!queue.isEmpty()) {
            GraphNode n = queue.remove();
            for (GraphNode neighbor : n.neighbors) {
                if (neighbor.level == Integer.MIN_VALUE) {
                    neighbor.level = n.level + 1;
                    queue.add(neighbor);
                }
                if (neighbor.level == n.level + 1) {
                    neighbor.numPaths += n.numPaths;
                }
            }
        }

        System.out.println("numPaths to a: " + a.numPaths);
        System.out.println("numPaths to b: " + b.numPaths);
        System.out.println("numPaths to c: " + c.numPaths);
        System.out.println("numPaths to d: " + d.numPaths);
        System.out.println("numPaths to e: " + e.numPaths);
        System.out.println("numPaths to f: " + f.numPaths);
        System.out.println("numPaths to g: " + g.numPaths);
        System.out.println("numPaths to h: " + h.numPaths);
    }
}
```

### Compiler

- To execute this code, just copy paste it to [this online Java compiler](https://www.tutorialspoint.com/compile_java_online.php)

### Time/Space Complexity

-  Time Complexity: O(m + n) due to BFS
- Space Complexity: O(m + n) due to creation of graph

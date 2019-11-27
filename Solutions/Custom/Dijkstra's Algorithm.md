### Notes

I came up with this representation of the graph (using parallel arrays to make representing edges easy). There may be better ways to organize this data.

Dijkstra's algorithm will actually calculate the shortest path from a source node to _every_ other node in the graph.

### Sample Graph we will use

Letters are Nodes. Numbers are edge weights.
```
     1       5       4       6
 a ----- b ----- c ----- d ----- f
         |       |               |
       7 |       | 9             | 5
         |       |               |
         e ----- g ------------- h
             2           12
```


### Solution

```java
class GraphNode { // public variables for simplicity
    char data;
    boolean visited = false;
    List<GraphNode> neighbors = new ArrayList(); // parallel arrays
    List<Integer> edgeWeights = new ArrayList(); // parallel arrays
    int distance = Integer.MAX_VALUE;
    GraphNode parent = null;

    public GraphNode(char data) {
        this.data = data;
    }

    public void addNeighbor(GraphNode neighbor, int weight) {
        addDirectedNeighbor(neighbor, weight);
        neighbor.addDirectedNeighbor(this, weight);
    }

    public void addDirectedNeighbor(GraphNode neighbor, int weight) {
        neighbors.add(neighbor);
        edgeWeights.add(weight);
    }

    @Override
    public String toString() {
        return "data = " + data + "  visited = " + visited;
    }
}
```

```java
import java.util.*;

public class Dijkstra {
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
         a.addNeighbor(b, 1);
         b.addNeighbor(c, 5);
         c.addNeighbor(d, 4);
         d.addNeighbor(f, 6);
         b.addNeighbor(e, 7);
         e.addNeighbor(g, 2);
         c.addNeighbor(g, 9);
         g.addNeighbor(h, 12);
         h.addNeighbor(f, 5);

         // Initialize Start Node and insert into PriorityQueue
         PriorityQueue<GraphNode> distances = new PriorityQueue<>((n1, n2) -> n1.distance - n2.distance);
         e.distance = 0;
         e.visited = true;
         distances.add(e);

         // Dijkstra's Algorithm
         while (!distances.isEmpty()) {
             GraphNode v = distances.remove();
             v.visited = true;
             for (int i = 0; i < v.neighbors.size(); i++) {
                 GraphNode w = v.neighbors.get(i);
                 if (!w.visited) {
                     distances.add(w);
                     int edgeWeight = v.edgeWeights.get(i);
                     if (v.distance + edgeWeight < w.distance) {
                         w.distance = v.distance + edgeWeight;
                         w.parent = v;
                     }
                 }
             }
         }

         printSolution(a);
         printSolution(b);
         printSolution(c);
         printSolution(d);
         printSolution(f);
         printSolution(g);
         printSolution(h);
         return;
     }

     static void printSolution(GraphNode node) {
         System.out.println("\n--- Destination = " + node.data);
         while (node != null) {
             System.out.println(node);
             node = node.parent;
         }
     }
}
```

### Compiler

- To execute this code, just copy paste it to [this online Java compiler](https://www.tutorialspoint.com/compile_java_online.php)

### Time/Space Complexity

-  Time Complexity: O(m + n log n)
- Space Complexity: O(n)

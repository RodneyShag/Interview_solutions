### Tips

- Solution is from Jeff Erickson's Algorithms.pdf, Section 19.5 Topological Sort

### Solution

```java
enum Visited {
    NEW, ACTIVE, DONE
}

// using public variables for simplicity
@ToString
class Node {
    public char data;
    public Visited status;
    public ArrayList<Node> neighbors; // could alternatively use a HashSet (if I give nodes unique IDs)

    /* Constructor */
    public Node(char data) {
        this.data = data;
        status = Visited.NEW;
        neighbors = new ArrayList<>();
    }

    public void addDirectedNeighbor(Node neighbor) {
        neighbors.add(neighbor);
    }
}

ArrayDeque<Node> topologicalSort(List<Node> nodes) throws Exception {
    /* Create new "source" Node which has a directed edge to each node in our original graph */
    Node source = new Node('s');
    for (Node node : nodes) {
        source.addDirectedNeighbor(node);
    }

    ArrayDeque<Node> result = new ArrayDeque<>();
    topoSortDFS(source, result);
    result.removeFirst(); // removes the source node we created
    return result;
}

private void topoSortDFS(Node n, ArrayDeque<Node> result) throws Exception {
    n.status = Visited.ACTIVE;
    for (Node neighbor : n.neighbors) {
        if (neighbor.status == Visited.NEW) {
            topoSortDFS(neighbor, result);
        } else if (neighbor.status == Visited.ACTIVE) {
            throw new Exception("Not a DAG");
        }
    }
    n.status = Visited.DONE;
    result.addFirst(n);
}
```

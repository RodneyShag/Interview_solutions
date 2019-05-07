### Notes

- Solution is from Jeff Erickson's Algorithms.pdf, Section 19.5 Topological Sort
- Code uses classes with public variables for simplicity

### Solution

```java
enum Visited {
    NEW, ACTIVE, DONE
}
```

```java
class Node { // public variables for convenience
    public String data;
    public Visited status;
    public ArrayList<Node> neighbors; // could alternatively use a HashSet (if I give nodes unique IDs)

    public Node(String data) {
        this.data = data;
        status = Visited.NEW;
        neighbors = new ArrayList<>();
    }

    public void addDirectedNeighbor(Node neighbor) {
        neighbors.add(neighbor);
    }
}
```

```java
class Graph {
    public List<Node> nodes = new ArrayList<>();
    public Map<String, Node> map = new HashMap<>();

    public void addDirectedEdge(String s1, String s2) {
        Node source = map.get(s1);
        Node destination = map.get(s2);
        source.addDirectedNeighbor(destination);
    }

    public void addNode(String str) {
        Node node = new Node(str);
        nodes.add(node);
        map.put(str, node);
    }
}
```

```java
class BuildOrder {
    // Converts our inconveniently formatted input into a graph
    public ArrayDeque<Node> topoSort(String[] projects, String[][] dependencies) throws Exception {
        Graph graph = new Graph();
        for (String project : projects) {
            graph.addNode(project);
        }
        for (String[] dependency : dependencies) {
            String source = dependency[0];
            String destination = dependency[1];
            graph.addDirectedEdge(source, destination);
        }
        return topoSort(graph);
    }

    private ArrayDeque<Node> topoSort(Graph graph) throws Exception {
        Node source = new Node("Source");
        for (Node node : graph.nodes) {
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
                throw new Exception("Not a DAG. Graph has a cycle.");
            }
        }
        n.status = Visited.DONE;
        result.addFirst(n);
    }
}
```

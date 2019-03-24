### Provided code

Let's assume we're given the following `Node` class, with variables marked `public` for simplicity.

```java
class Node {
    public Node next;
    public int data ;
    public Node(int d) {
      next = null;
      data = data;
    }
}
```

### Solution

```java
class Stack {
    private Node top = null;

    public void push(int data) {
        Node n = new Node(data);
        n.next = top;
        top = n;
    }

    public Node pop() {
        if (top == null) {
            return null;
        }
        Node n = top;
        top = top.next;
        n.next = null; // rips off the node from the Stack
        return n;
    }

    public Node peek() {
        return top;
    }
}
```

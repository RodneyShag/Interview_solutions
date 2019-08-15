### Provided code

Let's assume we're given the following `Node` class:

```java
class Node { // public variables for simplicity
    Node next;
    int data ;
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

### Time/Space Complexity

-  Time Complexity: O(1) for push(), pop(), peek().
- Space Complexity: O(1) for push(), pop(), peek(). O(1) to store each Node permanently.

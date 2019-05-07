### Tips

- Ask if it's a "Singly-Linked List" or "Doubly-Linked List" (We implement a SLL below)

### Solution

```java
class Node {
    public Node next = null;
    public int data = 0;

    public Node(int d) {
        data = d;
    }

    public void appendToTail(int d) {
        Node n = this; // slick move
        while (n.next != null) {
            n = n.next;
        }
        n.next = new Node(d);
    }
}
```

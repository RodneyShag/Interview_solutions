### Tips

- Ask if it's a "Singly-Linked List" or "Doubly-Linked List" (We implement a SLL below)

### Solution

```java
class Node { // public variables used for simplicity
    Node next = null;
    int data = 0;

    public Node(int d) {
        data = d;
    }
}
```

```java
public class SinglyLinkedList { // public variables used for simplicity
    Node head = null;
    Node tail = null;

    public void addFirst(Node n) {
        if (n == null) {
            return;
        }
        if (head == null) { // list is empty
            head = n;
            tail = n;
        } else {
            n.next = head;
            head = n;
        }
    }

    public void addLast(Node n) {
        if (n == null) {
            return;
        }
        if (tail == null) { // list is empty
            head = n;
            tail = n;
        } else {
            tail.next = n;
            tail = n;
        }
    }
}
```

### Notes

Many more methods can be implemented, such as `size()`, `removeFirst()`, `set(int index, E element)`, `get(int index)`.

### Solution

```java
class Node { // public variables for simplicity
    Node next;
    int data ;
    public Node(int d) {
      next = null;
      data = d;
    }
}
```

```java
class Queue {
    private Node head = null;
    private Node tail = null;

    public void add(int data) {
        Node n = new Node(data);
        if (head == null) {
            head = n;
            tail = n;
        } else {
            tail.next = n;
            tail = n;
        }
    }

    public Node remove() {
        if (head == null) {
            return null; // list is empty
        }
        Node front = head;
        head = head.next;
        if (head == null) {
            tail = null;
        }
        front.next = null; // rips the Node from the Queue
        return front;
    }

    public Node peek() {
        return head;
    }
}
```

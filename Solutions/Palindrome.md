### Provided code

Let's assume we're given the following `Node` class, with variables marked `public` for simplicity.

```java
class Node {
    public Node next = null;
    public int data = 0;
}
```

### Solution 1

```java
boolean palindrome(Node head) {
    int size = ListFunctions.calculateSize(head);
    ArrayDeque<Integer> deque = new ArrayDeque<>();
    Node curr = head;
    /* Save 1st half of list */
    for (int i = 0; i < size / 2; i++) {
        deque.push(curr.data);
        curr = curr.next;
    }
    /* If list had odd number of elements -> skip middle element */
    if (size % 2 == 1) {
        curr = curr.next;
    }
    /* Compare 2nd half of list to 1st half of list */
    while (curr != null) {
        if (deque.pop() != curr.data) {
            return false;
        }
        curr = curr.next;
    }
    return true;
}
```

- Time Complexity: O(n)
- Space Complexity: O(n)

### Solution 2

1. Deep copy list.
1. Reverse it.
1. Compare it to original.


- Time Complexity: O(n)
- Space Complexity: O(n)

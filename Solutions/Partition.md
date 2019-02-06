#### Provided code

Let's assume we're given the following `Node` class, with variables marked `public` for simplicity.
```java
class Node {
    public Node next = null;
    public int data = 0;
}
```

#### Solution 1

Same idea as Quicksort's partition() function

```java
Node partition(Node head, int x) {
    Node curr = head;
    Node p = head;
    while (curr != null) {
        if (curr.data < x) {
            /* Swap DATA values */
            int temp = p.data;
            p.data = curr.data;
            curr.data = temp;

            p = p.next;
        }
        curr = curr.next;
    }
    return head;
}
```

- Time Complexity: O(n)
- Space Complexity: O(1)

#### Solution 2

If swapping data is not allowed, we can Create 2 SLLs from a SLL, and connect them.

```java
Node partition(Node n, int x) {
    Node head1 = null;
    Node head2 = null;
    Node tail1 = null; // to walk list1
    Node tail2 = null; // to walk list2

    while (n != null) {
        if (n.data < x) {
            if (head1 == null) {
                head1 = n;
                tail1 = n;
            } else {
                tail1.next = n;
                tail1 = n;
            }
        } else {
            if (head2 == null) {
                head2 = n;
                tail2 = n;
            } else {
                tail2.next = n;
                tail2 = n;
            }
        }
        n = n.next;
    }

    if (tail2 != null) {
        tail2.next = null;
    }

    if (head1 == null) {
        return head2;
    } else {
        tail1.next = head2;
        return head1;
    }
}
```

- Time Complexity: O(n)
- Space Complexity: O(1)

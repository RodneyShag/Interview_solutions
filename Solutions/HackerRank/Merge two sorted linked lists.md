#### Provided code

```java
class Node {
    int data;
    Node next;
}
```

#### Solution

```java
SinglyLinkedListNode mergeLists(SinglyLinkedListNode currA, SinglyLinkedListNode currB) {
    if (currA == null) {
        return currB;
    } else if (currB == null) {
        return currA;
    }

    /* Find new head pointer */
    SinglyLinkedListNode head = null;
    if (currA.data < currB.data) {
        head = currA;
        currA = currA.next;
    } else {
        head = currB;
        currB = currB.next;
    }

    /* Build rest of list */
    SinglyLinkedListNode n = head;
    while (currA != null && currB != null) {
        if (currA.data < currB.data) {
            n.next = currA;
            currA = currA.next;
        } else {
            n.next = currB;
            currB = currB.next;
        }
        n = n.next;
    }

    /* Attach the remaining elements */
    if (currA == null) {
        n.next = currB;
    } else {
        n.next = currA;
    }

    return head;
}
```

#### Time/Space complexity

- Time Complexity: O(n + m)
- Space Complexity: O(1)

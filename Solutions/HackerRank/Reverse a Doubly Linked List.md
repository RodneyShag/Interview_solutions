#### Provided code

```java
class DoublyLinkedListNode {
    int data;
    DoublyLinkedListNode next;
    DoublyLinkedListNode prev;
}
```

#### Solution

```java
DoublyLinkedListNode reverse(DoublyLinkedListNode head) {
    if (head == null && head.next == null) {
        return head;
    }
    DoublyLinkedListNode prev = null;
    DoublyLinkedListNode curr = head;
    DoublyLinkedListNode next = null;
    while (curr != null) {
        next = curr.next;
        curr.next = prev;
        curr.prev = next;
        prev = curr;
        curr = next;
    }
    return prev;
}
```

#### Time/Complexity

-  Time Complexity: O(n)
- Space Complexity: O(1)

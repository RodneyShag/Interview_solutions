#### Solution

```java
SinglyLinkedListNode reverse(SinglyLinkedListNode head) {
    if (head == null && head.next == null) {
        return head;
    }
    SinglyLinkedListNode prev = null;
    SinglyLinkedListNode curr = head;
    SinglyLinkedListNode next = null;
    while (curr != null) {
        next = curr.next;
        curr.next = prev; // changes arrow direction
        prev = curr;
        curr = next;
    }
    return prev;
}
```

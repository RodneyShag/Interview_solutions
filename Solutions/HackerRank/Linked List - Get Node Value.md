#### Provided Code

```java
class SinglyLinkedListNode {
    int data;
    SinglyLinkedListNode next;
}
```

#### Solution

```java
int getNode(SinglyLinkedListNode head, int positionFromTail) {
    SinglyLinkedListNode curr   = head;
    SinglyLinkedListNode runner = head;

    /* Move runner into the list by k elements */
    for (int i = 0; i < positionFromTail; i++) {
        runner = runner.next;
    }

    /* Move both pointers */
    while (runner.next != null) {
        curr   = curr.next;
        runner = runner.next;
    }

    return curr.data;
}
```

#### Time/Space complexity

- Time Complexity: O(n)
- Space Complexity: O(1)

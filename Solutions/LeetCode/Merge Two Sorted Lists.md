### Provided code

```java
class ListNode {
    int val;
    ListNode next;
    ListNode(int x) { val = x; }
}
```

### Solution

```java
ListNode mergeTwoLists(ListNode currA, ListNode currB) {
    if (currA == null) {
        return currB;
    } else if (currB == null) {
        return currA;
    }

    /* Find new head pointer */
    ListNode head = null;
    if (currA.val < currB.val) {
        head = currA;
        currA = currA.next;
    } else {
        head = currB;
        currB = currB.next;
    }

    /* Build rest of list */
    ListNode n = head;
    while (currA != null && currB != null) {
        if (currA.val < currB.val) {
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

### Time/Space Complexity

- Time Complexity: O(n + m)
- Space Complexity: O(1)

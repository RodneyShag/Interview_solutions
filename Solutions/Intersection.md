#### Provided code

Let's assume we're given the following `Node` class, with variables marked `public` for simplicity.
```java
class Node {
    public Node next = null;
    public int data = 0;
}
```

#### Algorithm

Create a pointer that iterates through a list. When it's at the end of the list, have it jump to the beginning of the other list. Create 2 of these pointers, pointing to 2 different list heads. The pointers will collide at the merge point after 1 or 2 passes. If they don't, then there is no merge point.

#### Solution

```java
Integer findMergeNode(Node headA, Node headB) {
    Node currA = headA;
    Node currB = headB;

    int jumps = 0;
    while (currA != currB) {
        if (currA.next == null) {
            currA = headB;
            jumps++;
        } else {
            currA = currA.next;
        }

        if (currB.next == null) {
            currB = headA;
            jumps++;
        } else {
            currB = currB.next;
        }
        if (jumps > 2) {
            return null; // they don't intersect
        }
    }
    return currA.data;
}
```

#### Time/Space Complexity

- Time Complexity: O(n)
- Space Complexity: O(1)

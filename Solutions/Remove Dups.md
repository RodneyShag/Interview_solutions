### Provided code

Let's assume we're given the following `Node` class, with variables marked `public` for simplicity.
```java
class Node {
    public Node next = null;
    public int data = 0;
}
```

### Solution

```java
void removeDuplicates(Node head) {
    HashSet<Integer> set = new HashSet<>();
    set.add(head.data);
    Node n = head;
    while (n.next != null) {
        if (set.contains(n.next.data)) {
            n.next = n.next.next;
        } else {
            set.add(n.next.data);
            n = n.next;
        }
    }
    return;
}
```

### Time/Space Complexity

- Time Complexity: O(n)
- Space Complexity O(n)

### Alternate Solution

- Brute-force compare all pairs (Advantage is low space complexity). Use 1 pointer to walk list, and another pointer to check all remaining nodes each time.
- Time Complexity: O(n<sup>2</sup>)
- Space Complexity: O(1)

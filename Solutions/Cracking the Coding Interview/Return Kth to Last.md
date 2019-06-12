### Algorithm

Just calculate the size of the SLL, then walk `size - k` elements into the list

### Solution

```java
class Node {
    Node next = null;
    int data = 0;
    public Node(int d) {
        data = d;
    }
}
```

```java
int calculateSize(Node head) {
    if (head == null) {
        return 0;
    }
    Node n = head;
    int size = 1;
    while (n.next != null) {
        n = n.next;
        size++;
    }
    return size;
}
```

```java
Node kthLast(Node n, int k) {
    int size = calculateSize(n);
    if (k <= 0 || k > size) {
        return null;
    }
    for (int i = 0; i < size - k; i++) {
        n = n.next;
    }
    return n;
}
```

### Time/Space Complexity

- Time Complexity: O(n)
- Space Complexity: O(1)

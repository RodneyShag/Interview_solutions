### Solution

```java
boolean deleteMid(Node n) {
    if (n == null || n.next == null) { // this algorithm only works if we are deleting an element that's not the last element.
        return false;                  // Otherwise, we can maybe just mark that last element as a "Dummy", according to textbook.
    }
    n.data = n.next.data;
    n.next = n.next.next;
    return true;
}
```

- Time complexity: O(1) - simply move the data.

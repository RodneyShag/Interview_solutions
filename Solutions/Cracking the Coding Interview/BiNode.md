### Solution

```java
class BiNode { // public variables for simplicity
    BiNode left, right;
    int data;

    public BiNode(int d) {
        left  = null;
        right = null;
        data  = d;
    }
}
```

```java
class Converter {
    BiNode head = null;
    BiNode tail = null;

    public void inorderTraverse(BiNode root) {
        if (root != null) {
            inorderTraverse(root.left);
            buildList(root);
            inorderTraverse(root.right);
        }
    }

    private void buildList(BiNode n) {
        if (head == null || tail == null) {
            head = tail = n;
            n.left = n.right = null;
        } else {
            tail.right = n;
            n.left = tail;
            tail = n;
        }
    }
}
```

### Time/Space Complexity

-  Time Complexity: O(n)
- Space Complexity: O(n)

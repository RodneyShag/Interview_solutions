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
    public static BiNode head = null;
    public static BiNode tail = null;

    public static void inorderTraverse(BiNode root) {
        if (root != null) {
            inorderTraverse(root.left);
            buildList(root);
            inorderTraverse(root.right);
        }
    }

    private static void buildList(BiNode n) {
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

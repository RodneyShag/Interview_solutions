#### Notes

- This problem defines a 1-Node tree to have height of 1

#### Solution

```java
int maxDepth(TreeNode root) {
    if (root == null) {
        return 0;
    } else {
        return 1 + Math.max(maxDepth(root.left), maxDepth(root.right));
    }
}
```

### Provided Code

[TreeNode](https://github.com/RodneyShag/Interview_solutions/blob/master/Solutions/Cracking%20the%20Coding%20Interview/Implement%20a%20TreeNode.md)

### Solution

```java
isBST(TreeNode root) {
    return isBST(root, Integer.MIN_VALUE, Integer.MAX_VALUE);
}

private boolean isBST(TreeNode node, int min, int max) {
    if (node == null) {
        return true;
    }
    if (node.data <= min || node.data > max) { // tricky off-by-one errors for duplicates. Tricky whether it's <, <=, >, >=
        return false;
    }
    return isBST(node.left, min, node.data) && isBST(node.right, node.data, max);
}
```

### Time/Space Complexity

-  Time Complexity: O(n) since we visit every node
- Space Complexity: Space Complexity: O(log n) if tree is balanced, O(n) otherwise, since that's the depth of the recursion.

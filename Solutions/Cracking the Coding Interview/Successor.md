### Provided Code

- [TreeNode](https://github.com/RodneyShag/Interview_solutions/blob/master/Solutions/Cracking%20the%20Coding%20Interview/Implement%20a%20TreeNode.md)

### Tips

- Read Cracking the Coding Interview's logic, but ignore its code. The code below is much cleaner.
- Notice there are 2 distinct cases: `leftMostChild()`, and `properParent()`

### Solution

```java
TreeNode inOrderSucc(TreeNode node) {
    if (node.right != null) {
        return leftMostChild(node.right);
    } else {
        return properParent(node);
    }
}

private TreeNode leftMostChild(TreeNode node) {
    if (node == null) {
        return null;
    }
    TreeNode result = node;
    while (result.left != null) {
        result = result.left;
    }
    return result;
}

// Finds the parent (well, ancestor) that has treeNode in its left subtree. Returns null if such parent doesn't exist
private TreeNode properParent(TreeNode node) {
    if (node == null) {
        return null;
    }
    TreeNode parent = node.parent;
    TreeNode child = node;
    while (parent != null && parent.left != child) {
        child = parent; // crucial step
        parent = child.parent;
    }
    return parent;
}
```

### Additional Notes

Finding Successor of a Node is useful when deleting a node in a binary *search* tree, since that's a node we can put in place of the deleted node

### Time/Space Complexity

-  Time Complexity: O(n)
- Space Complexity: O(1)

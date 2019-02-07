#### Provided Code

- [TreeNode](https://github.com/RodneyShag/Interview_solutions/blob/master/Solutions/Implement%20a%20TreeNode.md)

#### Tips

- Read Cracking the Coding Interview's logic, but ignore its code. The code below is much cleaner.
- Notice there are 2 distinct cases: `leftMostChild()`, and `properParent()`

#### Solution

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

/* Finds the parent (well, ancestor) that has treeNode in its left subtree. Returns null if such parent doesn't exist */
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

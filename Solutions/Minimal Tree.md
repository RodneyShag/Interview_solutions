### Provided Code

- [TreeNode](https://github.com/RodneyShag/Interview_solutions/blob/master/Solutions/Implement%20a%20TreeNode.md)

### Solution

```java
TreeNode createBST(int[] sortedArray) {
    return createBST(sortedArray, 0, sortedArray.length - 1);
}

private TreeNode createBST(int[] sortedArray, int startIndex, int endIndex) {
    if (startIndex > endIndex) {
        return null;
    }
    int mid = (startIndex + endIndex) / 2;
    TreeNode root = new TreeNode(sortedArray[mid]);
    root.left  = createBST(sortedArray, startIndex, mid - 1);
    root.right = createBST(sortedArray, mid + 1, endIndex);
    return root;
}
```

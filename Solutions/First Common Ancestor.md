### Notes

This question can be similarly phrased as "Find a path from one node in a binary tree to another"

### Provided Code

- [TreeNode](https://github.com/RodneyShag/Interview_solutions/blob/master/Solutions/Implement%20a%20TreeNode.md)


### List of Solutions

| # |        Solutions        |        Runtime       |   Preference    |
|:-:|:-----------------------:|:--------------------:|:---------------:|
| 0 | If BST, trace Paths     | O(log n) if balanced |     Clever      |
| 1 | Use links to parents    | O(log n) if balanced |     Clever      |
| 2 | Recursive               | O(n)                 |     Favorite    |


### Solution 0

If tree is a Binary Search Tree, can go down the tree from the root to see where we need to diverge paths.


### Solution 1

If we have links to parents, we can save all of node1's parents (ancestors) in a HashSet and then see if node2's parents (ancestors) match any of those.


### Solution 2

- From [LeetCode](http://www.programcreek.com/2014/07/leetcode-lowest-common-ancestor-of-a-binary-tree-java/)

```java
TreeNode commonAnc(TreeNode root, TreeNode p, TreeNode q) {
    if (root == null) {
        return null;
    } else if (root == p || root == q) {
        return root;
    }

    TreeNode left  = commonAnc(root.left, p, q);
    TreeNode right = commonAnc(root.right, p, q);

    if (left == null) {
        return right;
    } else if (right == null) {
        return left;
    } else {
        return root;
    }
}
```

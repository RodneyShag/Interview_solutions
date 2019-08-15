### Solution

This represents a binary Tree. If we wanted an n-ary tree, we would use an array of `TreeNode`s as children

```java
@Getter
@ToString
public class TreeNode {
    private TreeNode left   = null;
    private TreeNode right  = null;
    private TreeNode parent = null; // optional
    private int data;

    public TreeNode(int data) {
        this.data = data;
    }

    public void addLeftChild(int data) {
        TreeNode node = new TreeNode(data);
        left = node;
        node.parent = this;
    }

    public void addRightChild(int data) {
        TreeNode node = new TreeNode(data);
        right = node;
        node.parent = this;
    }
}
```

### Time/Space Complexity

- Time Complexity: O(1) for TreeNode(), addLeftChild(), addRightChild().
- Space Complexity: O(1) for TreeNode(), addLeftChild(), addRightChild(). Each TreeNode requires O(1) storage for itself.

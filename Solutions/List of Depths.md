#### Solution

```java
ArrayList<LinkedList<TreeNode>> createLists(TreeNode root) {
    ArrayList<LinkedList<TreeNode>> lists = new ArrayList<>();
    createListsHelper(root, lists, 0);
    return lists;
}

private void createListsHelper(TreeNode node, ArrayList<LinkedList<TreeNode>> lists, int currLevel) {
    if (node == null) {
        return;
    }

    /* Tricky. May need a new list for a new level */
    if (lists.size() == currLevel) { // levels are visited in order, so this should work.
        lists.add(new LinkedList<TreeNode>());
    }

    /* Add this Node */
    LinkedList<TreeNode> list = lists.get(currLevel); // get the appropriate list to add the node to.
    list.add(new TreeNode(node.data)); // DEEP COPY - don't forget!

    /* Recursively add this nodes subtrees */
    createListsHelper(node.left, lists, currLevel + 1);
    createListsHelper(node.right, lists, currLevel + 1);
}
```

#### Tricky Implementation Details
1. Knowing to return an "ArrayList<LinkedList<Node>>".
1. Knowing that, to alter the "ArrayList<LinkedList<Node>>", we should pass it as a parameter so it can be altered.
1. Know to also pass the "level" down the tree.
1. Remembering to create new LinkedLists in our ArrayList when necessary.
1. Making a DEEP COPY whenever we add Nodes to the list.

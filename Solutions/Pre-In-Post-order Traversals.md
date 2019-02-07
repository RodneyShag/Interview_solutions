#### Provided Code

- [TreeNode](https://github.com/RodneyShag/Interview_solutions/blob/master/Solutions/Implement%20a%20TreeNode.md)

#### Solution

```java
void printPreOrder(TreeNode node) {
    if (node != null) {
        System.out.print(node);
        printPreOrder(node.getLeft());
        printPreOrder(node.getRight());
    }
}

void printInOrder(TreeNode node) {
    if (node != null) {
        printInOrder(node.getLeft());
        System.out.print(node);
        printInOrder(node.getRight());
    }
}

void printPostOrder(TreeNode node) {
    if (node != null) {
        printPostOrder(node.getLeft());
        printPostOrder(node.getRight());
        System.out.print(node);
    }
}
```

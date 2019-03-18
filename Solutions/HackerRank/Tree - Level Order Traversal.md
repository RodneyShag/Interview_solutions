#### Provided Code

```java
class Node {
    int data;
    Node left;
    Node right;
}
```

#### Solution

```java
void LevelOrder(Node root) {
    ArrayDeque<Node> deque = new ArrayDeque<>(); // use deque as a queue
    if (root != null) {
        deque.add(root);
    }
    while (!deque.isEmpty()) {
        Node n = deque.remove();
        System.out.print(n.data + " ");
        if (n.left != null) {
            deque.add(n.left);
        }
        if (n.right != null) {
            deque.add(n.right);
        }
    }
}
```

#### Time/Space Complexity

- Time Complexity: O(n)
- Space Complexity: O(n)

### Question

Consider a simple data structure called `BiNode`, which has pointers to two other nodes.

```java
public class BiNode {
    public BiNode nodel, node2;
    public int data;
}
```

The data structure `BiNode` could be used to represent both a binary tree (where nodel is the left node and node2 is the right node) or a doubly linked list (where nodel is the previous node and node2 is the next node). Implement a method to convert a binary search tree (implemented with `BiNode`) into a doubly linked list. The values should be kept in order and the operation should be performed in place (that is, on the original data structure)

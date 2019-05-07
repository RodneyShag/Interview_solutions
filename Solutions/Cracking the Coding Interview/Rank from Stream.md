### Analysis of Data Structures we can use

|   Data Structure   | Insert (into sorted structure) |                              getRank()                                    |
|:------------------:|:------------------------------:|:-------------------------------------------------------------------------:|
| Array              | O(n) due to shifting           | O(log n) using binary search                                              |
| Linked List        | O(n)                           | O(n) since we can't do binary search on linked list                       |
| HashMap            | O(1)                           | O(n) since HashMap doesn't help us find rank in any way (it's not sorted) |
| Binary Search Tree | O(log n)                       | O(log n) (assuming it's balanced)                                         |
### Solution

```java
class RankNode {
    int data;
    RankNode left;
    RankNode right;
    int leftSize; // each RankNode will keep track of the number of RankNodes in its left subtree

    public RankNode(int data) {
        this.data = data;
        left = null;
        right = null;
        leftSize = 0;
    }
}
```

```java
class RankFromStream {

    private static RankNode root = null;

    /* Called each time a number is generated */
    public static void track(int x) {
        if (root == null) {
            root = new RankNode(x);
        } else {
            insert(x, root);
        }
    }

    private static void insert(int x, RankNode node) {
        if (x <= node.data) {
            node.leftSize++;
            if (node.left == null) {
                node.left = new RankNode(x);
            } else {
                insert(x, node.left);
            }
        } else {
            if (node.right == null) {
                node.right = new RankNode(x);
            } else {
                insert(x, node.right);
            }
        }
    }

    /* Returns number of values less than or equal to x (not including x itself) */
    public static int getRankOfNumber(int x) {
        if (root == null) {
            return 0;
        }
        return getRankOfNumber(x, root);
    }

    private static int getRankOfNumber(int x, RankNode node) {
        if (node == null) {
            return 0;
        } else if (x == node.data) {
            return node.leftSize;
        } else if (x > node.data) {
            return 1 + node.leftSize + getRankOfNumber(x, node.right);
        } else {
            return getRankOfNumber(x, node.left);
        }
    }
}
```

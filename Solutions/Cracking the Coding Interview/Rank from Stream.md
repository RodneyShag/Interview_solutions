### Analysis of Data Structures we can use

|   Data Structure   | Insert (into sorted structure) |                              getRank()                                    |
|:------------------:|:------------------------------:|:-------------------------------------------------------------------------:|
| Array              | O(n) due to shifting           | O(log n) using binary search                                              |
| Linked List        | O(n)                           | O(n) since we can't do binary search on linked list                       |
| HashMap            | O(1)                           | O(n) since HashMap doesn't help us find rank in any way (it's not sorted) |
| Binary Search Tree | O(log n) (if balanced tree)    | O(log n) (if balanced tree)                                               |

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

    private RankNode root = null;

    // Called each time a number is generated
    public void track(int x) {
        if (root == null) {
            root = new RankNode(x);
        } else {
            insert(x, root);
        }
    }

    private void insert(int x, RankNode root) {
        RankNode curr = root;
        while (true) {
            if (x <= curr.data) {
                curr.leftSize++;
                if (curr.left == null) {
                    curr.left = new RankNode(x);
                    return;
                } else {
                    curr = curr.left;
                }
            } else {
                if (curr.right == null) {
                    curr.right = new RankNode(x);
                    return;
                } else {
                    curr = curr.right;
                }
            }
        }
    }

    // Returns number of values less than or equal to x (not including x itself)
    public int getRankOfNumber(int x) {
        if (root == null) {
            return 0;
        }
        RankNode curr = root;
        int rank = 0;
        while (curr != null) {
            if (x == curr.data) {
                return rank + curr.leftSize;
            } else if (x > curr.data) {
                rank += 1 + curr.leftSize;
                curr = curr.right;
            } else {
                curr = curr.left;
            }
        }
        return 0;
    }
}
```

### Time/Space Complexity

-  Time Complexity: `insert()`, `getRankOfNumber()` are O(log n) if tree is balanced. O(n) otherwise. If we implemented more advanced trees, such as "AVL trees", then we could ensure the tree stays balanced.
- Space Complexity: `insert()`, `getRankOfNumber()` are O(1) since they're coded iteratively. O(1) space is also required to store each `RankNode`

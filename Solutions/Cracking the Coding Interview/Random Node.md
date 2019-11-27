### Algorithm

1. To have getRandomNode() in O(1) time, we want to put all the nodes in a collection that does add(), remove(), contains(), and getRandom() all in O(1) time. [This question](https://leetcode.com/problems/insert-delete-getrandom-o1-duplicates-allowed) and [solution](https://github.com/RodneyShag/Interview_solutions/blob/master/Solutions/LeetCode/Insert%20Delete%20GetRandom%20O%281%29%20-%20Duplicates%20allowed.md) provide this `RandomizedCollection` data structure for us.
1. Code a standard Binary Search Tree (BST), and on each insert into the BST, also insert into the `RandomizedCollection`.
1. Implementation Detail: To be able to put `Node` into a `HashSet`, we had to include the `equals()` and `hashCode()` methods.

### Solution

```java
class Node {
    int value;
    Node left;
    Node right;

    Node(int value) {
        this.value = value;
        left = null;
        right = null;
    }

    @Override
    public boolean equals(Object other) { // must take an "Object" as a parameter, not a
                                          // "Node", so that it overrides the .equals() method
        if (other == this) {
            return true;
        } else if (other == null || !(other instanceof Node)) {
            return false;
        }
        Node otherNode = (Node) other;
        return this.value == otherNode.value
            && this.left.equals(otherNode.left)
            && this.right.equals(otherNode.right);
    }

    @Override
    public int hashCode() {
        return value; // since only using 1 int, won't be multiplying by primes.
    }

    @Override
    public String toString() {
        return String.valueOf(value);
    }
}
```

```java
public class RandomizedCollection<T> {
    Random rand = new Random();
    List<T> list = new ArrayList();
    Map<T, Set<Integer>> valToIndices = new HashMap();

    public void add(T item) {
        // update Map
        if (!valToIndices.containsKey(item)) {
            valToIndices.put(item, new HashSet());
        }
        valToIndices.get(item).add(list.size());

        // update List
        list.add(item);

        return;
    }

    public boolean remove(T item) {
        if (!valToIndices.containsKey(item) || valToIndices.get(item).isEmpty()) {
            return false;
        }

        int indexToRemove = valToIndices.get(item).iterator().next();
        T itemLast = list.get(list.size() - 1);

        // update List
        list.set(indexToRemove, itemLast);
        list.remove(list.size() - 1);

        // update Map: remove overwritten index from set
        valToIndices.get(item).remove(indexToRemove);

        // update Map: update the moved number's index
        valToIndices.get(itemLast).add(indexToRemove);                              
        valToIndices.get(itemLast).remove(list.size());

        return true;
    }

    public boolean contains(T item) {
        return valToIndices.containsKey(item) && !valToIndices.get(item).isEmpty();
    }

    public T getRandom() {
        if (list.isEmpty()) {
            throw new Error("Collection is empty");
        }
        int index = rand.nextInt(list.size());
        return list.get(index);
    }
}
```

```java
class BST {
    Node root = null;
    RandomizedCollection<Node> collection = new RandomizedCollection();

    public void insert(int value) {
        Node item = new Node(value);

        // Update collection
        collection.add(item);

        // Update tree
        if (root == null) {
            root = item;
            return;
        }
        Node curr = root;
        while (true) {
            if (value <= curr.value) {
                if (curr.left == null) {
                    curr.left = item;
                    return;
                } else {
                    curr = curr.left;
                }
            } else {
                if (curr.right == null) {
                    curr.right = item;
                    return;
                } else {
                    curr = curr.right;
                }
            }
        }
    }

    // doing O(log n) traversal for practice. Alternatively, save a HashMap<Integer, Node> for O(1) time.
    public Node find(int value) {
        Node curr = root;
        while (curr != null) {
            if (value == curr.value) {
                return curr;
            } else if (value < curr.value) {
                curr = curr.left;
            } else {
                curr = curr.right;
            }
        }
        return null;
    }

    public Node getRandomNode() {
        return collection.getRandom();
    }
}
```

### delete()

- Problem also asks us to code delete() for a node in the tree
- To delete, can find "inorder successor" of the node to delete, and put that in deleted node's spot. See [Cracking the Coding Interview question 4.6](https://github.com/RodneyShag/Interview_solutions/blob/master/Solutions/Cracking%20the%20Coding%20Interview/Successor.md)
- For deletion of Node, see 1-3 at [Geeks For Geeks](https://www.geeksforgeeks.org/binary-search-tree-set-2-delete/)

### Time Complexity

- insert()
  - O(log n) for BST.
  - O(1) for add to `RandomizedCollection`
- find()
  - O(log n) if traversing tree.
  - O(1) if using HashMap<Integer, Node> instead of traversal.
- getRandomNode(): O(1)

### Space Complexity

O(1) for each Node

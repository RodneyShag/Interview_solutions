### Algorithm

```
           50
         /    \
       20      60
      /   \      \
    10     25     70
   /   \         /   \
  5    15       65    80
```
Since this tree was made by "traversing through an array from left to right and inserting each element", then

- the first element in our array must be 50.
- Once 50 is inserted, all items less than 50 will be routed to the left and all items greater than 50 will be
routed to the right. The 60 or the 20 could be inserted first, and it wouldn't matter.

If we had all arrays that could create the subtree rooted at 20, and all arrays that could create the subtree rooted at 60, then we could "weave" these arrays together in every possible combination, and prepend 50 to each result.

### Provided Code

[TreeNode](https://github.com/RodneyShag/Interview_solutions/blob/master/Solutions/Cracking%20the%20Coding%20Interview/Implement%20a%20TreeNode.md)

### Solution

```java
List<Deque<Integer>> allSequences(TreeNode node) {
    List<Deque<Integer>> results = new ArrayList();

    if (node == null) {
        results.add(new ArrayDeque<Integer>()); // crucial. So the code labeled "weave lists" works properly
        return results;
    }

    Deque<Integer> prefix = new ArrayDeque();
    prefix.add(node.data);

    // Recursive Cases
    List<Deque<Integer>> leftSeq  = allSequences(node.left);
    List<Deque<Integer>> rightSeq = allSequences(node.right);

    // Weave lists
    for (Deque<Integer> left : leftSeq) {
        for (Deque<Integer> right : rightSeq) {
            weaveLists(left, right, results, prefix);
        }
    }

    return results;
}

private void weaveLists(Deque<Integer> list1, Deque<Integer> list2,
                List<Deque<Integer>> results, Deque<Integer> prefix) {
    // Base Case
    if (list1.isEmpty() || list2.isEmpty()) {
        Deque<Integer> result = new ArrayDeque<>(prefix);
        result.addAll(list1);
        result.addAll(list2);
        results.add(result);
        return;
    }

    // Use 1st entry in list1
    Integer temp = list1.removeFirst();
    prefix.addLast(temp);
    weaveLists(list1, list2, results, prefix);
    prefix.removeLast();
    list1.addFirst(temp);

    // Use 1st entry in list2
    temp = list2.removeFirst();
    prefix.addLast(temp);
    weaveLists(list1, list2, results, prefix);
    prefix.removeLast();
    list2.addFirst(temp);
}
```

### Time Complexity

This is very difficult to compute. Here is my guess:

`weaveLists` is O(2<sup>n</sup>) where `n` is length of the 2 lists combined. This is because at each step we have 2 choices as to which entry to use next, so there are O(2<sup>n</sup>) nodes in our recursion tree.

An alternative way to represent `weaveLists` runtime is "(m + n) choose (n)" (based off [this post](https://stackoverflow.com/questions/21211701/given-a-bst-and-its-root-print-all-sequences-of-nodes-which-give-rise-to-the-sa/24398114#24398114)), but even this runtime could be tigher since it hasn't taken into account that the `n` elements need to come in a certain order.too.

`allSequences` has a recursion tree that visits `n` nodes. Each "for" loop adds a factor of O(2<sup>n</sup>), and weaveLists adds a factor of O(2<sup>n</sup>). So we get O(n2<sup>n</sup>2<sup>n</sup>2<sup>n</sup>) = O(n2<sup>3n</sup>) = __O(n2<sup>n</sup>)__

### Space Complexity

My guess is that the space complexity is the same as time complexity here, since we save all solutions. This gives us __O(n2<sup>n</sup>)__ as there are O(2<sup>n</sup>) solutions, each taking up O(n) space.

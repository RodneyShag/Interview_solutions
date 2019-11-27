### Algorithm

Use "Backtracking" - an algorithm for finding all solutions by exploring all potential candidates.

This is the same as the [Permutations](https://leetcode.com/problems/permutations) problem, except that we use a `Set` to remove duplicates.

### Solution

```java
class Solution {
    public List<List<Integer>> permuteUnique(int[] array) {
        if (array == null || array.length == 0) {
            return new ArrayList();
        }
        Set<List<Integer>> solutions = new HashSet();
        permute(array, 0, new boolean[array.length], solutions, new ArrayList());
        return new ArrayList<>(solutions);
    }

    private void permute(int[] array, int index, boolean[] used, Set<List<Integer>> solutions, List<Integer> list) {
        if (index == array.length) {
            solutions.add(new ArrayList<>(list));
            return;
        }
        for (int i = 0; i < array.length; i++) {
            if (used[i] == false) {
                list.add(array[i]);
                used[i] = true;
                permute(array, index + 1, used, solutions, list);
                used[i] = false;
                list.remove(list.size() - 1);
            }
        }
    }
}
```

### Time/Space Complexity

If you view this recursion as a tree, there will be `n!` leaf nodes, so there are O(n!) nodes in total. At each node, we do O(n) work looping through the array. So our runtime is O(n * n!).

-  Time Complexity: O(n * n!)
- Space Complexity: O(n * n!)

### Similar BackTracking Problems

- [Permutations](https://leetcode.com/problems/permutations)
- [Subsets](https://leetcode.com/problems/subsets) and [Subsets II](https://leetcode.com/problems/subsets-ii)
- [Letter Combinations of a Phone Number](https://leetcode.com/problems/letter-combinations-of-a-phone-number)
- [N-Queens](https://leetcode.com/problems/n-queens)

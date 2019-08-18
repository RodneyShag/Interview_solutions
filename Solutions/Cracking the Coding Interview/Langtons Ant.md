### Solution

Main trick: Instead of representing the grid as a 2-D array, use a `Set<Position> whites` to keep track of White squares, where `Position` contains a `row` and `col`, and also has `equals()` and `hashCode()` methods overriden.

If a Position is not in the `HashSet`, it is a black square.

Ant starts at Position(0,0).

### Time/Space Complexity

If `n` is number of moves, we have

-  Time Complexity: O(n), as each move takes O(1) time.
- Space Complexity: O(n) to store in our HashSet.

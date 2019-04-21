### Algorithm

- Loop through our `char[][] grid`, and for each piece of land we see (a `1`), we mark all the land it's connected to.
- We mark land by simply changing the `1` in our `grid` to a `0`.
- To keep track of __distinct__ shapes, we keep track of the path we took when exploring an island
  - since we always explore in the same method (Up, Down, Left, Right), matching paths will represent matching shapes.
  - to save path, make sure to record both 1) how we enter function, and 2) when we exit function

### Code

```java
public int numIslands(char[][] grid) {
    if (grid == null || grid.length == 0) {
        return 0;
    }
    final int rows = grid.length;
    final int cols = grid[0].length;

    Set<String> paths = new HashSet<>();

    for (int row = 0; row < rows; row++) {
        for (int col = 0; col < cols; col++) {
            if (grid[row][col] == '1') {
                StringBuffer path = new StringBuffer("S"); // S for Start
                explore(grid, row, col, rows, cols, path);
                paths.add(path.toString());
            }
        }
    }
    return paths.size();
}

private void explore(char[][] grid, int row, int col, int rows, int cols, StringBuffer path) {
    if (row < 0 || row >= rows || col < 0 || col >= cols || grid == null || grid[row][col] == '0') {
        return;
    }

    grid[row][col] = '0'; // we alter the original matrix here

    // Recursively search neighbors
    explore(grid, row - 1, col, rows, cols, path.append("U")); // Up
    explore(grid, row + 1, col, rows, cols, path.append("D")); // Down
    explore(grid, row, col - 1, rows, cols, path.append("L")); // Left
    explore(grid, row, col + 1, rows, cols, path.append("R")); // Right
    path.append("_"); // crucial step
    return;
}
```

### Time/Space Complexity

- Time Complexity: O(rows * cols)
- Space Complexity: O(rows * cols)

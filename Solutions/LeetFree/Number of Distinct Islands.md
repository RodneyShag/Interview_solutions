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

    Set<String> paths = new HashSet();

    for (int r = 0; r < rows; r++) {
        for (int c = 0; c < cols; c++) {
            if (grid[r][c] == '1') {
                StringBuffer path = new StringBuffer("S"); // S for Start
                explore(grid, r, c, rows, cols, path);
                paths.add(path.toString());
            }
        }
    }
    return paths.size();
}

private void explore(char[][] grid, int r, int c, int rows, int cols, StringBuffer path) {
    if (r < 0 || r >= rows || c < 0 || c >= cols || grid == null || grid[r][c] == '0') {
        return;
    }

    grid[r][c] = '0'; // we alter the original matrix here

    // Recursively search neighbors
    explore(grid, r - 1, c, rows, cols, path.append("U")); // Up
    explore(grid, r + 1, c, rows, cols, path.append("D")); // Down
    explore(grid, r, c - 1, rows, cols, path.append("L")); // Left
    explore(grid, r, c + 1, rows, cols, path.append("R")); // Right
    path.append("_"); // crucial step
    return;
}
```

### Time/Space Complexity

- Time Complexity: O(rows * cols)
- Space Complexity: O(rows * cols)

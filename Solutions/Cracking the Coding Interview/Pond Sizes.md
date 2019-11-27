### Solution

```java
List<Integer> findPonds(int[][] grid) {
    List<Integer> pondSizes = new ArrayList();
    int rows = grid.length;
    int cols = grid[0].length;
    for (int row = 0; row < rows; row++) {
        for (int col = 0; col < cols; col++) {
            if (grid[row][col] == 0) {
                int pondSize = findPondSize(grid, row, col, rows, cols);
                pondSizes.add(pondSize);
            }
        }
    }
    return pondSizes;
}

private int findPondSize(int[][] grid, int row, int col, int rows, int cols) {
    if (row < 0 || row >= rows || col < 0 || col >= cols || grid[row][col] != 0) {
        return 0;
    }

    grid[row][col] = -1; // marks as visited
    int pondSize = 1;    // 1 accounts for our size
    for (int r = row - 1; r <= row + 1; r++) {
        for (int c = col - 1; c <= col + 1; c++) {
            pondSize += findPondSize(grid, r, c, rows, cols);
        }
    }
    return pondSize;
}
```

### Time/Space Complexity

-  Time Complexity: O(rows * cols)
- Space Complexity: O(rows * cols) since that's the max size of `List<Integer> pondSizes`, and is also the max depth of our recursion

#### Solution 0

- Binary search every row for O(m log n) runtime. Not coding this solution since Solution 1 (below) is more efficient.

#### Solution 1

- On every step, eliminate a row or a column.
  - Start in top right corner
  - Always either move down (eliminating current row), or move left (eliminating current col)
  - Alternate solution: start in bottom left and move to top right

```java
boolean findElement(int[][] grid, int elem) {
    int rows = grid.length;
    int cols = grid[0].length;

    /* Start at top right corner */
    int row = 0;
    int col = cols - 1;

    while (row < rows && col >= 0) {
        if (grid[row][col] == elem) {
            return true;
        } else if (grid[row][col] > elem) {
            col--;
        } else {
            row++;
        }
    }
    return false;
}
```

- Time Complexity: O(m+n)

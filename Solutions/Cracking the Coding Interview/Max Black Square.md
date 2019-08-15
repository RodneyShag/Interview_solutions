### Tricks

1. Preprocess the grid
1. Have `Cell` and `Subsquare` classes
1. Search largest squares first

### Solution

```java
class Cell {
    public int blacksRight = 0; // including itself
    public int blacksDown  = 0; // including itself

    public Cell(int right, int below) {
        blacksRight = right;
        blacksDown  = below;
    }
}
```

```java
Subsquare findLargestSubsquare(int[][] grid) { // O(n) * runtime of findSubSquare()
    Cell[][] processed = preprocessGrid(grid);
    for (int dimension = processed.length; dimension >= 1; dimension--) {
        Subsquare subsquare = findSubsquare(processed, dimension);
        if (subsquare != null) {
            return subsquare;
        }
    }
    return null;
}

Cell[][] preprocessGrid(int[][] grid) { // O(n^2)
    int rows = grid.length;
    int cols = grid[0].length;

    Cell[][] preprocessed = new Cell[rows][cols];
    for (int r = rows - 1; r >= 0; r--) {
        for (int c = cols - 1; c >= 0; c--) {
            preprocessed[r][c] = new Cell(0, 0);
            if (grid[r][c] == 1) {
                preprocessed[r][c].blacksRight = 1 + ((c + 1 < cols) ? preprocessed[r][c + 1].blacksRight : 0);
                preprocessed[r][c].blacksDown  = 1 + ((r + 1 < rows) ? preprocessed[r + 1][c].blacksDown  : 0);
            }
        }
    }
    return preprocessed;
}

private Subsquare findSubsquare(Cell[][] cellMatrix, int length) { // O(n^2) (since 2 for loops)
    int wiggleRoom = cellMatrix.length - length;

    for (int startRow = 0; startRow <= wiggleRoom; startRow++) {
        for (int startCol = 0; startCol <= wiggleRoom; startCol++) {
            if (isValidSquare(cellMatrix, startRow, startCol, length)) {
                return new Subsquare(startRow, startCol, length);
            }
        }
    }
    return null;
}

private boolean isValidSquare(Cell[][] cellMatrix, int row, int col, int length) { // O(1)
    Cell topLeft     = cellMatrix[row][col];
    Cell topRight    = cellMatrix[row][col + length - 1];
    Cell bottomLeft  = cellMatrix[row + length - 1][col];
    Cell bottomRight = cellMatrix[row + length - 1][col + length - 1];
    if (topLeft.blacksDown < length || topLeft.blacksRight < length) {
        return false;
    } else if (topRight.blacksDown < length || topRight.blacksRight < 1) {
        return false;
    } else if (bottomLeft.blacksDown < 1 || bottomLeft.blacksRight < length) {
        return false;
    } else if (bottomRight.blacksDown < 1 || bottomRight.blacksRight < 1) {
        return false;
    }
    return true;
}
```

### Time/Space Complexity

- Time Complexity: O(n<sup>3</sup>)
- Space Complexity: O(n<sup>2</sup>)

### Algorithm

1. Preprocess all possible boards to create a 1-1 mapping from boards to integers: 0 to maxNumBoards
1. Use an array of booleans to indicate which boards are winning boards.

Checking a board to see if there's a winner is done by checking `n` rows, `n` cols, and 2 diagonals (code omitted here)

### Solution

```java
class TicTacWin {
    private boolean[] winnerMap; // assume this array has been filled with proper values.

    private int convertBoardToInt(char[][] board) {
        int sum = 0;
        int factor = 1;
        int dimension = board.length; // assumes square board
        for (int row = 0; row < dimension; row++) {
            for (int col = 0; col < dimension; col++) {
                char ch = board[row][col];
                int value = 0;
                switch (ch) {
                    case ' ':
                        value = 0 * factor;
                        break;
                    case 'o':
                        value = 1 * factor;
                        break;
                    case 'x':
                        value = 2 * factor;
                        break;
                    default: // should not occur
                        break;
                }
                sum += value;
                factor *= dimension;
            }
        }
        return sum;
    }

    public boolean hasWon(char[][] board) {
        return winnerMap[convertBoardToInt(board)];
    }
}
```

### Time Complexity

- There are O(3<sup>n<sup>2</sup></sup>) boards to preprocess. For each board, validating if there's a winner takes O(n<sup>2</sup>) time. So preprocessing takes __O(n<sup>2</sup>3<sup>n<sup>2</sup></sup>)__ time
- __O(n<sup>2</sup>)__ for `convertBoardToInt()`, `hasWon()`.

### Space Complexity

O(3<sup>n<sup>2</sup></sup>) since that's the number of possible boards

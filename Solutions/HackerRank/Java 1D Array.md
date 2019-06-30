### Solution

```java
boolean canWin(int leap, int[] game) {
    if (game == null) {
        return false;
    }
    return isSolvable(leap, game, 0);
}

private boolean isSolvable(int leap, int[] game, int i) {
    // Base Cases
    if (i >= game.length) {
        return true;
    } else if (i < 0 || game[i] == 1) {
        return false;
    }

    game[i] = 1; // marks as visited

    // Recursive Cases (Tries +leap first to try to finish game quickly)
    return isSolvable(leap, game, i + leap)
        || isSolvable(leap, game, i + 1)
        || isSolvable(leap, game, i - 1);
}
```

### Time/Space Complexity

-  Time Complexity: `O(n)`. We will only try each position in the game once since we mark spots as "visited".
- Space Complexity: `O(n)` due to recursion

### Solution

```java
boolean canWin(int leap, int[] game) {
    return isSolvable(leap, game, 0);
}

private boolean isSolvable(int leap, int[] game, int i) {
    // Base Cases
    if (i < 0 || game[i] == 1) {
        return false;
    } else if (i + 1 >= game.length || i + leap >= game.length) {
        return true;
    }

    game[i] = 1; // marks as visited

    // Recursive Cases (Tries +leap first to try to finish game quickly)
    return isSolvable(leap, game, i + leap)
        || isSolvable(leap, game, i + 1)
        || isSolvable(leap, game, i - 1);
}
```

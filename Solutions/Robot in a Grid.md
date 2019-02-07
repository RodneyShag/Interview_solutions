#### Solution

There are `x+y` moves total. Choose `x` of them to go right. So it's `x+y` choose `x` (The combinations formula), giving:
```
 (x+y)!  
--------
(x!)(y!)
```

```java
int numPaths(int cols, int rows) {
    int[][] paths = new int[rows][cols];

    /* Base cases */
    for (int row = 0; row < rows; row++) {
        paths[row][0] = 1;
    }
    for (int col = 0; col < cols; col++) {
        paths[0][col] = 1;
    }

    /* Memoize 2-D array */
    for (int row = 1; row < rows; row++) {
        for (int col = 1; col < cols; col++) {
            paths[row][col] = paths[row - 1][col] + paths[row][col - 1];
        }
    }
    return paths[rows - 1][cols - 1];
}
```

#### Follow-up Solution

- I search from end to start (makes code simpler to write)
- The reason we use a HashMap as a cache instead of an int[][] is because HashMap can give us 3 pieces of information:
  1. Not in cache  -> we have to try searching from here
  1. cached, false -> path doesn't exist
  1. cached, true  -> path exists

```java

public ArrayList<Point> findPath(final boolean[][] maze, int row, int col) {
    if (maze == null || row < 0 || row >= maze.length || col < 0 || col >= maze[0].length) {
        return null;
    }

    /* Create path to save solution into */
    ArrayList<Point> path = new ArrayList<>();
    path.add(new Point(0, 0));

    /* Create cache to save solutions to subproblems */
    HashMap<Point, Boolean> cache = new HashMap<>(); // requires overriding .equals() and .hashCode for Point, for HashMap to work properly
    cache.put(new Point(0, 0), true); // base case

    /* Recursively calculate answer */
    boolean foundResult = findPath(maze, row, col, path, cache);
    if (foundResult) {
        return path;
    } else {
        return null;
    }
}

private boolean findPath(final boolean[][] maze, int row, int col, ArrayList<Point> path, HashMap<Point, Boolean> cache) {
    Point p = new Point(col, row);
    if (cache.containsKey(p)) { // here so that we don't recompute subproblems that we already solved
        return cache.get(p);    // since nobody is going to alter the Point p, no need to do a deep copy before returning cached result
    }

    if (!isFree(maze, row, col)) {
        return false;
    }

    /* Find paths recursively. Tricky to remember to only search the 2nd path if necessary */
    boolean success = findPath(maze, row, col - 1, path, cache);
    if (!success) {
        success = findPath(maze, row - 1, col, path, cache); // if no success, we try moving vertically
    }

    cache.put(p, success); // update cache

    /* Update path if we found a solution */
    if (success) {
        path.add(p);
    }

    return success;
}

/* A spot is free if it's within maze bounds and is not a wall */
private boolean isFree(boolean[][] maze, int row, int col) {
    if (row < 0 || row >= maze.length || col < 0 || col >= maze[0].length) {
        return false;
    }
    return maze[row][col];
}
```

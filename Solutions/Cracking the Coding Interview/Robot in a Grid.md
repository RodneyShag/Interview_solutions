### Algorithm

- I search from end to start (makes code simpler to write)
- The reason we use a HashMap as a cache instead of an int[][] is because HashMap can give us 3 pieces of information:
  1. Not in cache  -> we have to try searching from here
  1. cached, false -> path doesn't exist
  1. cached, true  -> path exists

### Solution

- [How to write equals method in java](http://javarevisited.blogspot.com/2011/02/how-to-write-equals-method-in-java.html)
- [override hashcode in java example](http://javarevisited.blogspot.com/2011/10/override-hashcode-in-java-example.html)

```java
public class Point {
    public int x;
    public int y;

    Point(int x, int y) {
        this.x = x;
        this.y = y;
    }

    @Override
    public boolean equals(Object other) { // must take an "Object" as a parameter, not a
                                          // "Point" so that it overrides the .equals method
        if (other == this) {
            return true;
        } else if (other == null || !(other instanceof Point)) {
            return false;
        }
        Point otherPoint = (Point) other;
        return this.x == otherPoint.x && this.y == otherPoint.y;
    }

    @Override
    public int hashCode() {
        return 13 * x + 7 * y;
    }
}
```

```java
public List<Point> findPath(final boolean[][] maze, int row, int col) {
    if (maze == null || row < 0 || row >= maze.length || col < 0 || col >= maze[0].length) {
        return null;
    }

    // Create path to save solution into
    List<Point> path = new ArrayList<>();
    path.add(new Point(0, 0));

    // Create cache to save solutions to subproblems
    Map<Point, Boolean> cache = new HashMap<>(); // requires overriding .equals() and .hashCode for Point, for HashMap to work properly
    cache.put(new Point(0, 0), true); // base case

    // Recursively calculate answer
    boolean foundResult = findPath(maze, row, col, path, cache);
    if (foundResult) {
        return path;
    } else {
        return null;
    }
}

private boolean findPath(final boolean[][] maze, int row, int col, List<Point> path, Map<Point, Boolean> cache) {
    Point p = new Point(col, row);
    if (cache.containsKey(p)) { // here so that we don't recompute subproblems that we already solved
        return cache.get(p);    // since nobody is going to alter the Point p, no need to do a deep copy before returning cached result
    }

    if (!isFree(maze, row, col)) {
        return false;
    }

    // Find paths recursively. Tricky to remember to only search the 2nd path if necessary
    boolean success = findPath(maze, row, col - 1, path, cache);
    if (!success) {
        success = findPath(maze, row - 1, col, path, cache); // if no success, we try moving vertically
    }

    cache.put(p, success); // update cache

    // Update path if we found a solution
    if (success) {
        path.add(p);
    }

    return success;
}

// A spot is free if it's within maze bounds and is not a wall
private boolean isFree(boolean[][] maze, int row, int col) {
    if (row < 0 || row >= maze.length || col < 0 || col >= maze[0].length) {
        return false;
    }
    return maze[row][col];
}
```

### Time/Space Complexity

- Time Complexity: O(rows * cols)
- Space Complexity: O(rows * cols)

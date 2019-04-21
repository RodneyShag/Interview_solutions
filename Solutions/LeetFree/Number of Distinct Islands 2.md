### Algorithm

- Loop through our `char[][] grid`, and for each piece of land we see (a `1`), we mark all the land it's connected to.
- We mark land by simply changing the `1` in our `grid` to a `0`.
- The transformations/rotations correspond to doing the following to all points:
  1. (x, y)
  1. (x, -y)
  1. (-x, y)
  1. (-x, -y)
  1. (y, x)
  1. (y, -x)
  1. (-y, x)
  1. (-y, -x)
- Since each shape has 8 possible shapes, we create a "canonical key", meaning all 8 shapes will match to this same canonical key

### Solution

```java
class Point implements Comparable<Point> {
    // public access for simplicity
    public int x;
    public int y;

    public Point(int x, int y) {
        this.x = x;
        this.y = y;
    }

    @Override
    public int compareTo(Point other) {
        if (this.x == other.x) {
            return Integer.compare(this.y, other.y);
        } else {
            return Integer.compare(this.x, other.x);
        }
    }
}

public class Solution {
    private int rows;
    private int cols;

    public int numIslands(char[][] grid) {
        if (grid == null || grid.length == 0) {
            return 0;
        }
        rows = grid.length;
        cols = grid[0].length;

        Set<List<Point>> islands = new HashSet<>();

        // save all islands
        for (int row = 0; row < rows; row++) {
            for (int col = 0; col < cols; col++) {
                if (grid[row][col] == '1') {
                    List<Point> island = new ArrayList<>();
                    explore(grid, row, col, island);
                    islands.add(island);
                }
            }
        }

        Set<String> uniqueIslands = new HashSet<>();
        for (List<Point> island : islands) {
            Set<List<Point>> eightShapes = rotateAndReflect(island);
            String key = generateKey(eightShapes);
            uniqueIslands.add(key);
        }

        return uniqueIslands.size();
    }

    private void explore(char[][] grid, int row, int col, List<Point> island) {
        if (row < 0 || row >= rows || col < 0 || col >= cols || grid == null || grid[row][col] == '0') {
            return;
        }

        grid[row][col] = '0'; // we alter the original matrix here
        island.add(new Point(row, col));

        // Recursively search neighbors
        explore(grid, row - 1, col, island);
        explore(grid, row + 1, col, island);
        explore(grid, row, col - 1, island);
        explore(grid, row, col + 1, island);
        return;
    }

    // Rotate and reflect a given shape to 8 possible shapes
    private Set<List<Point>> rotateAndReflect(List<Point> shape) {
        Map<Integer, List<Point>> map = new HashMap<>();
        for (int i = 0; i < 8; i ++) {
            map.put(i, new ArrayList<>());
        }
        for (Point point : shape) {
            map.get(0).add(new Point(point.x, point.y));
            map.get(1).add(new Point(-point.x, point.y));
            map.get(2).add(new Point(point.x, -point.y));
            map.get(3).add(new Point(-point.x, -point.y));
            map.get(4).add(new Point(point.y, point.x));
            map.get(5).add(new Point(-point.y, point.x));
            map.get(6).add(new Point(point.y, -point.x));
            map.get(7).add(new Point(-point.y, -point.x));
        }
        return new HashSet<>(map.values());
    }

    private String generateKey(Set<List<Point>> eightShapes) {
        List<String> keys = new ArrayList<>();
        for (List<Point> shape : eightShapes) {
            Collections.sort(shape);
            Point first = shape.get(0);
            keys.add(shape.stream()
                        .map(p -> new Point(p.x - first.x, p.y - first.y))
                        .map(p -> p.x + ":" + p.y)
                        .collect(Collectors.joining(",")));
        }
        Collections.sort(keys);
        return keys.get(0);
    }
}
```

### Time/Space Complexity

- Time Complexity: O(n log n) which is due to sorting, where max value of `n` is (number of columns) * (number of rows)
- Space Complexity: O(rows * cols)

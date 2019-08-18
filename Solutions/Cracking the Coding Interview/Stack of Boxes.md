### Algorithm

Based off Cracking the Coding Interview 6th Edition's Solution 1. This is a Dynamic Programming Recursive solution, using `HashMap` as a cache.

We assume rotation of a box is not allowed.

1. Create Box class with `.canBeAbove(Box other)` function.
2. Sort Boxes in descending height order. This ensures we don't have to look backwards in the list.
    - This problem uses `<` instead of `<=` for Box heights. If we have 2 Boxes of equal height,
      such as [width, height, depth] of [4,4,4] and [7,4,7], it doesn't matter which Box comes first
      after sorting, since both Boxes can't be in the final solution. Box 1 cannot be on top of Box 2,
      and Box 2 cannot be on top of Box 1.
3. Experiment with each Box as a bottom and build the biggest stack possible.
4. Use a "Map<Integer, Integer>" cache to save solutions to sub-problems.
    1. "key" is the index `i` in the List of boxes.
    2. "value" is the max height possible with "Box i" at the bottom.

### Solution

```java
public class Box {
    int width;
    int height;
    int depth;

    Box(int w, int h, int d) {
        width  = w;
        height = h;
        depth  = d;
    }

    public boolean canBeAbove(Box other) {
        return (other == null) || (width < other.width && height < other.height && depth < other.depth);
    }

    @Override
    public String toString() {
        return "Box (" + width + "," + height + "," + depth + ")";
    }
}
```

```java
public class StackOfBoxes {
    public int findMaxHeight(List<Box> boxes) {
        if (boxes == null || boxes.size() == 0) {
            return 0;
        }
        Collections.sort(boxes, (box1, box2) -> box2.height - box1.height); // sort in descending height order
        return findMaxHeight(boxes, -1, new HashMap<Integer, Integer>());
    }

    private int findMaxHeight(List<Box> boxes, int bottomIndex, Map<Integer, Integer> cache) {
        if (cache.containsKey(bottomIndex)) {
            return cache.get(bottomIndex);
        }

        int maxHeight = 0;
        Box bottom = bottomIndex == -1 ? null : boxes.get(bottomIndex);

        for (int i = bottomIndex + 1; i < boxes.size(); i++) {
            if (boxes.get(i).canBeAbove(bottom)) {
                int height = findMaxHeight(boxes, i, cache);
                maxHeight = Math.max(maxHeight, height);
            }
        }

        maxHeight += bottomIndex == -1 ? 0 : bottom.height;
        cache.put(bottomIndex, maxHeight);
        return maxHeight;
    }
}
```

### Time/Space Complexity

-  Time Complexity: O(n<sup>2</sup>)
- Space Complexity: O(n) due to recursion.

### Follow-up Question - What if rotation of boxes is allowed?

1. For each box, rotate it to all 6 possibilities: [w h d], [w d h], [h w d] [h d w], [d w h], [d h w].
1. Notice it's impossible to stack 2 of these 6 boxes on top of each other, so if we insert all 6 boxes into our list, we're still ensured only 1 of them can be selected for our solution.
1. Create `List<Box> boxes` that is 6 times as large as the original list of boxes. Solve the problem for this list.

Time/Space Complexity would remain the same.

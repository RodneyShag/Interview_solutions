### Algorithm

We assume rotation of a box is not allowed

1. Create `Box` class with `.canBeAbove(Box other)` function.
1. Sort `Box`es in descending height order.
    - This problem uses `<` instead of `<=` for `Box` heights. If we have 2 `Box`es of equal height, and `[width, height, depth]` of `[4,4,4]` and `[7,4,7]`, it doesn't matter which `Box` comes first after sorting, since both `Box`es can't be in the final solution. Box 1 cannot be on top of Box 2, and Box 2 cannot be on top of Box 1.
1. For each `Box`, you have 2 choices:
    1. Use the Box
    1. Don't use the Box.
1. Recursively try both options. Return the larger height returned from these 2 options.
1. Use a Map<Integer, Integer> cache to save solutions to sub-problems
    1. "key" is the index `i` in the list of boxes
    1. "value" is the max height possible from that Box to the end of our list of Boxes

### Solution - Dynamic Programming - Recursive using HashMap as Cache

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
}
```

```java
public class StackOfBoxes {
    public int findMaxHeight(List<Box> boxes) {
        if (boxes == null || boxes.size() == 0) {
            return 0;
        }
        Collections.sort(boxes, (box1, box2) -> box2.height - box1.height); // sort in descending height order
        return findMaxHeight(boxes, 0, null, new HashMap<>(boxes.size()));
    }

    private int findMaxHeight(List<Box> boxes, int i, Box bottom, Map<Integer, Integer> cache) {
        if (i >= boxes.size()) {
            return 0;
        } else if (cache.containsKey(i)) {
            return cache.get(i);
        }

        // height with this Box
        Box newBottom = boxes.get(i);
        int heightWith = 0;
        if (newBottom.canBeAbove(bottom)) {
            heightWith = newBottom.height + findMaxHeight(boxes, i + 1, newBottom, cache);
        }

        // height without this Box
        int heightWithout = findMaxHeight(boxes, i + 1, bottom, cache);

        int max = Math.max(heightWith, heightWithout);
        cache.put(i, max);
        return max;
    }
}
```

### Time/Space Complexity

-  Time Complexity: Without caching, the recursive part is O(2<sup>n</sup>) since there are `n` boxes, and 2 options for each box (use or don't use). With caching, the recursive part is just O(n). The total time complexity is therefore `O(n log n)` due to sorting.
- Space Complexity: `O(n)` due to recursion.

### Follow-up Question - What if rotation of boxes is allowed?

1. For each box, rotate it to all 6 possibilities: [w h d], [w d h], [h w d] [h d w], [d w h], [d h w].
1. Notice it's impossible to stack 2 of these 6 boxes on top of each other, so if we insert all 6 boxes into our list, we're still ensured only 1 of them can be selected for our solution.
1. Create `List<Box> boxes` that is 6 times as large as the original list of boxes. Solve the problem for this list.

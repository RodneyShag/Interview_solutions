#### Tips

- Have `Box` class with `.canBeAbove(Box other)` function.
- Use `HashMap<Box, ArrayDeque<Box>>` to cache found solutions. Need to override `.equals()` and `hashCode()`.
- Having `Box bottom` as a parameter is crucial but hard to think of.
- Deep copy (which is what I did) or cloning (which is what book did) is needed to avoid insidious bugs.

#### Solution

```java
@EqualsAndHashCode // I think this is needed so Boxes can be hashed correctly
@ToString
public class Box {
    int width;
    int height;
    int depth;

    /* Constructor */
    Box(int w, int h, int d) {
        width  = w;
        height = h;
        depth  = d;
    }

    /* Constructor */
    Box(Box other) {
        width  = other.width;
        height = other.height;
        depth  = other.depth;
    }

    /* A box can be placed on 1) an empty platform (that's what the "other == null" is for), or 2) a bigger box (in every dimension) */
    public boolean canPlaceAbove(Box other) {
        return (other == null) || (width < other.width && height < other.height && depth < other.depth);
    }
}
```

Solution based of __Cracking the Coding Interview__'s 2nd solution

```java
ArrayDeque<Box> buildTallestStack(ArrayDeque<Box> boxes) {
    return buildTallestStack(boxes, null, new HashMap<Box, ArrayDeque<Box>>());
}

private ArrayDeque<Box> buildTallestStack(ArrayDeque<Box> boxes, Box bottom, HashMap<Box, ArrayDeque<Box>> cache) {
    if (cache.containsKey(bottom)) { // checks to see if we already computed the solution
        /* CRUCIAL to do a deep copy. The result we return is going to be altered, and we don't want the key of an entry
           already placed in the HashMap to be altered. Without deep copy, we get incorrect solutions when testing */
        return deepCopy(cache.get(bottom));
    }

    int currHeight = 0;
    int bestHeight = 0;
    ArrayDeque<Box> currStack = new ArrayDeque<>();
    ArrayDeque<Box> bestStack = new ArrayDeque<>();

    for (Box box : boxes) {
        if (box.canPlaceAbove(bottom)) {
            currStack = buildTallestStack(boxes, box, cache);
            currHeight = stackHeight(currStack);
            if (currHeight > bestHeight) {
                bestHeight = currHeight;
                bestStack = currStack;
            }
        }
    }

    if (bottom != null) {
        bestStack.addFirst(bottom);
        cache.put(bottom, bestStack);
    }

    return bestStack;
}

private int stackHeight(ArrayDeque<Box> boxes) {
    if (boxes == null) {
        return 0;
    }
    int height = 0;
    for (Box box : boxes) {
        height += box.height;
    }
    return height;
}

private ArrayDeque<Box> deepCopy(ArrayDeque<Box> boxes) {
    ArrayDeque<Box> result = new ArrayDeque<>();
    for (Box box : boxes) {
        result.add(new Box(box));
    }
    return result;
}
```

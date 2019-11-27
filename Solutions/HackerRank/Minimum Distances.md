### Main trick

Use a `HashMap<Integer, Integer>` that maps from "value" to "index" to keep track
of the largest index for each value we've seen so far as we loop through array

### Solution

```java
int minimumDistances(int[] array) {
    Map<Integer, Integer> map = new HashMap();
    int minDistance = Integer.MAX_VALUE;
    for (int i = 0; i < array.length; i++) {
        if (map.containsKey(array[i])) {
            int prevIndex = map.get(array[i]);
            int currDistance = i - prevIndex;
            minDistance = Math.min(minDistance, currDistance);
        }
        map.put(array[i], i);
    }
    return minDistance == Integer.MAX_VALUE ? -1 : minDistance;
}
```

### Time/Space Complexity

- Time Complexity: O(n)
- Space Complexity: O(n)

### Solution

Use standard Binary Search - only works if no duplicate numbers.

```java
public Integer magicFast(int[] sortedArray) {
    int lo = 0;
    int hi = sortedArray.length - 1;

    while (lo <= hi) {
        int mid = (lo + hi) / 2;
        int midValue = sortedArray[mid];
        if (midValue == mid) {
            return mid;
        } else if (midValue > mid) {
            hi = mid - 1;
        } else {
            lo = mid + 1;
        }
    }
    return null;
}
```

### Time/Space Complexity

- Time Complexity: O(log n) on sorted array without duplicates
- Space Complexity: O(1)

### Follow-up Solution

If integers in sorted array are NOT UNIQUE, the best you get do is O(n) time complexity, O(1) space complexity by looping through every element in `sortedArray` in search of a solution.

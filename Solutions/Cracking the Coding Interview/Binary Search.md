### Solution

```java
Integer Iterative(int[] sortedArray, int value) {
    int start = 0;
    int end = sortedArray.length - 1;

    while (start <= end) {
        int mid = (start + end) / 2;
        if (sortedArray[mid] > value) {
            end = mid - 1;
        } else if (sortedArray[mid] < value) {
            start = mid + 1;
        } else {
            return mid;
        }
    }
    return null;
}
```

### Time/Space Complexity

- Time Complexity: O(log n)
- Space Complexity: O(1)

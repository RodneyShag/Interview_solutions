### Notes

A subarray must be contiguous. There are O(n^2) contiguous subarrays.

### Solution

```java
int negativeSubarrays(int[] array) {
    int count = 0;
    for (int i = 0; i < array.length; i++) {
        int sum = 0;
        for (int j = i; j < array.length; j++) {
            sum += array[j];
            if (sum < 0) {
                count++;
            }
        }
    }
    return count;
}
```

### Time/Space Complexity

- Time Complexity: O(n^2)
- Space Complexity: O(1)

### Notes

A subarray must be contiguous. There are O(n<sup>2</sup>) contiguous subarrays.

### Solution

```java
int subarraySum(int[] num, int k) {
    int count = 0;
    for (int i = 0; i < num.length; i++) {
        int sum = 0;
        for (int j = i; j < num.length; j++) {
            sum += num[j];
            if (sum == k) {
                count++;
            }
        }
    }
    return count;
}
```

### Time/Space Complexity

- Time Complexity: O(n<sup>2</sup>)
- Space Complexity: O(1)

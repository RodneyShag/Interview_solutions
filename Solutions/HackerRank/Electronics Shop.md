#### Algorithm

1. Sort both arrays.
1. Linearly walk through both arrays (at the same time).
  - If the combined price is unaffordable, find a cheaper harddrive `j--`
  - If the combined price is too low, update "max", and find a more expensive keyboard `i++`

#### Solution

```java
int getMoneySpent(int[] keyboards, int[] drives, int b) {
    Arrays.sort(keyboards); // O(n log n) time complexity
    Arrays.sort(drives);    // O(m log m) time complexity
    int max = -1;
    int i = 0;
    int j = drives.length - 1;
    while (i < keyboards.length && j >= 0) { // O(n + m) time complexity
        int cost = keyboards[i] + drives[j];
        if (cost > b) {
            j--; // look for a cheaper hard drive
        } else {
            if (cost > max) {
                max = cost;
            }
            i++; // look for a more expensive keyboard
        }
    }
    return max;
}
```

#### Time/Space Complexity

- Time Complexity: O(n log n + m log m)
- Space complexity: Depends on space complexity of `Arrays.sort()`

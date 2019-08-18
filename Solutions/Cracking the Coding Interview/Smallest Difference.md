### Tip

Kind of like a "2 sum" problem. Can call this a "Closest 2 sum" problem.

### Solution

```java
int smallestDifference(int[] array1, int[] array2) {
    Arrays.sort(array1);
    Arrays.sort(array2);
    int minDifference = Integer.MAX_VALUE;
    int i = 0;
    int j = 0;
    while (i < array1.length && j < array2.length) {
        int difference = Math.abs(array1[i] - array2[j]);
        minDifference = Math.min(minDifference, difference);
        if (array1[i] == array2[j]) {
            return 0;
        }
        if (array1[i] < array2[j]) {
            i++;
        } else {
            j++;
        }
    }
    return minDifference;
}
```

### Time Complexity

O(a log a + b log b) where a, b are lengths of the 2 arrays

### Space Complexity

Depends on Arrays.sort(). It's probably O(n), but can be as low as O(1) (if implemented using HeapSort)

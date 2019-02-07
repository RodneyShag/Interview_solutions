#### Solution

```java
void quickSort(int[] array) {
    if (array != null) {
        quickSort(array, 0, array.length - 1);
    }
}

private void quickSort(int[] array, int start, int end) {
    if (start < end) {
        int pivotIndex = partition(array, start, end);
        quickSort(array, start, pivotIndex - 1);
        quickSort(array, pivotIndex + 1, end);
    }
}

/* Partitions array into 2 parts.
 *   1) Left side has values smaller than pivotValue
 *   2) Right side has values larger than pivotValue
 * Returns pivotIndex
 */
private Integer partition(int[] array, int start, int end) {
    if (start > end) {
        return null;
    }
    int pivotIndex = (start + end) / 2; // there are many ways to choose a pivot
    int pivotValue = array[pivotIndex];

    swap(array, pivotIndex, end); // puts pivot at end for now.

    /* Linear search, comparing all elements to pivotValue and swapping as necessary */
    int indexToReturn = start; // Notice we set it to "start", not to "0".
    for (int i = start; i < end; i++) {
        if (array[i] < pivotValue) {
            swap(array, i, indexToReturn);
            indexToReturn++;
        }
    }

    swap(array, indexToReturn, end); // puts pivot where it belongs
    return indexToReturn;
}

private void swap(int[] array, int i, int j) {
    int temp = array[i];
    array[i] = array[j];
    array[j] = temp;
}
```

#### Time/Space Complexity

- Time Complexity
  - Worst Case - O(n<sup>2</sup>)
  - Average Case - O(n log n)
- Space Complexity: O(log n)

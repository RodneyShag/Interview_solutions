### Solution

```java
void mergeSort(int[] array) {
    if (array != null) {
        int[] helper = new int[array.length];
        mergeSort(array, helper, 0, array.length - 1);
    }
}

private void mergeSort(int[] array, int[] helper, int start, int end) {
    if (start < end) {
        int mid = (start + end) / 2;
        mergeSort(array, helper, start, mid);
        mergeSort(array, helper, mid + 1, end);
        merge(array, helper, start, mid, end);
    }
}

private void merge(int[] array, int[] helper, int start, int mid, int end) {
    for (int i = start; i <= end; i++) { // notice "i" goes from "start" to "end", not "0" to "array.length"
        helper[i] = array[i];
    }

    // Loop through helper[] left and right halves and continuously copy smaller element to array[]
    int curr = start;
    int left = start;
    int right = mid + 1;
    while (left <= mid && right <= end) {
        if (helper[left] <= helper[right]) {
            array[curr++] = helper[left++];
        } else {
            array[curr++] = helper[right++];
        }
    }

    // Copy remaining elements of left half. Right half elements are already in proper place (see book for explanation)
    while (left <= mid) {
        array[curr++] = helper[left++];
    }
}
```

### Time/Space Complexity

-  Time Complexity: O(n log n)
- Space Complexity: O(n)

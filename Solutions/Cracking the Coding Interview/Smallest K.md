# List of Solutions

- Let `m` be the million numbers and `n` be the billion numbers.

| # |  Solutions  |                    Runtime                       |    Preference    |
|:-:|:-----------:|:------------------------------------------------:|:----------------:|
| 0 | Sort        | O(n log n)                                       | Worth Mentioning |
| 1 | Max Heap    | O(n log m) (Notice it's "m" not "n")             | Worth Mentioning |
| 2 | QuickSelect | O(n) average case, O(n^2) worst case (bad pivot) |     Favorite     |


# Solution 0

Sort.


# Solution 1

Max Heap (Using PriorityQueue in Java, which has O(log m) for add() and remove())

Algorithm:

1. O(m) to build a MAX heap of first 1 million elements (using algo from CS 225), largest element at the top.
1. For each of the remaining "n" entries, if it's smaller than the heap's max element, we insert it into our heap by replacing the largest element (top of heap) with it. remove(), add() are O(log m), so total runtime O(n log m)


# Solution 2

### Algorithm

Use "QuickSelect"

- Finds "nth" smallest element in an array. Returns its value (Code from Wikipedia).
- Also partially sorts the data. If the value of the nth smallest element is x, all values to the left of it are smaller than x, and all values to the right of it are greater than x.

### Code

```java
Integer quickselect(int[] A, int n) {
    int lo = 0;
    int hi = A.length - 1;
    while (lo <= hi) {
        int pivotIndex = partition(A, lo, hi);
        if (pivotIndex == n) {
            return A[n];
        } else if (pivotIndex < n) {
            lo = pivotIndex + 1;
        } else {
            hi = pivotIndex - 1;
        }
    }
    return null;
}
```

- `partition()` partitions array into 2 parts.
    - Left side has values smaller than pivotValue
    - Right side has values larger than pivotValue
- Returns pivotIndex

```java
Integer partition(int[] A, int lo, int hi) {
    if (lo > hi) {
        return null;
    }
    int pivotIndex = (lo + hi) / 2; // there are many ways to choose a pivot
    int pivotValue = A[pivotIndex];

    swap(A, pivotIndex, hi); // puts pivot at end for now.

    // Linear search, comparing all elements to pivotValue and swapping as necessary
    int indexToReturn = lo;	// Notice we set it to "lo", not to "0".
    for (int i = lo; i < hi; i++) {
        if (A[i] < pivotValue) {
            swap(A, i, indexToReturn);
            indexToReturn++;
        }
    }

    swap(A, indexToReturn, hi); // puts pivot where it belongs
    return indexToReturn;
}

private void swap(int[] A, int i, int j) {
    int temp = A[i];
    A[i] = A[j];
    A[j] = temp;
}
```

Now just use QuickSelect to solve the problem.

```Java
void findNthSmallestNums(int[] array, int n) {
    quickselect(array, n);
    for (int i = 0; i < n; i++) {
        System.out.print(array[i] + " ");
    }
}
```

### Time Complexity

- `O(n)` average run-time since we divide the problem in half and only visit 1 side `n + n/2 + n/4 + ...) = n (1 + 1/2 + 1/4 + ...) = O(n)`. Our formula is a geometric series with `r = 1/2`, which would converge to `1/(1-r)` for infinite geometric series.
- O(n<sup>2</sup>) worst-case run-time is if "partition()" consistently picks a bad pivot. Can use [Median of Medians (MOM5)](https://en.wikipedia.org/wiki/Median_of_medians) to ensure good pivot choice, turning worst-case to O(n).

### Space Complexity

O(1)

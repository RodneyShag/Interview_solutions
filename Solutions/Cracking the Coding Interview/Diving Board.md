### Solution

```java
List<Integer> allLengths(int k, int shorter, int longer) {
    List<Integer> lengths = new ArrayList();
    for (int numShorter = 0; numShorter <= k; numShorter++) {
        int numLonger = k - numShorter;
        int length = numShorter * shorter + numLonger * longer;
        lengths.add(length);
    }
    return lengths;
}
```

### Time/Space Complexity

- Time Complexity: O(k)
- Space Complexity: O(k)

### Solution

```java
void toSwap(int[] arrayA, int[] arrayB) {
    int sum1 = Arrays.stream(arrayA).reduce(0, Integer::sum);
    int sum2 = Arrays.stream(arrayB).reduce(0, Integer::sum);
    if ((sum2 - sum1) % 2 != 0) {
        System.out.println("wont work");
        return;
    }
    int difference = (sum2 - sum1) / 2;
    Set<Integer> set = buildSet(arrayB);
    for (int numA : arrayA) {
        int neededNumB = numA + difference;
        if (set.contains(neededNumB)) {
            System.out.println("swap value " + numA + " from A\nwith value " + neededNumB + " from B");
            return;
        }
    }
    System.out.println("no solution");
}

private Set<Integer> buildSet(int[] array) {
    Set<Integer> set = new HashSet();
    for (int num : array) {
        set.add(num);
    }
    return set;
}
```

### Time/Space Complexity

-  Time complexity: O(a + b) where a, b are size of arrays
- Space Complexity: O(b). We could actually lower this to O(min(a, b)) by switching the arrays if `arrayA` is smaller.

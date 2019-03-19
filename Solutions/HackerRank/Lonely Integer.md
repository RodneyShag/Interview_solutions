### Notes

uses XOR. Keep in mind:

1. x ^ x = 0
1. x ^ 0 = x
1. XOR is commutative and associative

### Solution

```java
int findLonely(List<Integer> array) {
    int val = 0;
    for (int num : array) {
        val = val ^ num; // ^ is XOR operator
    }
    return val;
}
```

### Time/Space Complexity

- Time Complexity: O(n)
- Space Complexity: O(1)

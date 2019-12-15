### Solution

```java
boolean getBit(int n, int bit) {
    return (n & (1 << bit)) != 0;
}
```

### Time/Space Complexity

- Time Complexity: O(1)
- Space Complexity O(1)

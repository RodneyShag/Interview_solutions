### Solution

```java
boolean getBit(int num, int bit) {
    return (num & (1 << bit)) != 0;
}
```

### Time/Space Complexity

- Time Complexity: O(1)
- Space Complexity O(1)

### Solution

```java
int clearBit(int num, int bit) {
    int mask = ~(1 << bit);
    return num & mask;
}
```

### Time/Space Complexity

- Time Complexity: O(1)
- Space Complexity O(1)

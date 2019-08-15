### Solution

```java
boolean isRotation(String s1, String s2) {
    if (s1.length() != s2.length()) {
        return false;
    }
    String doubledString = s1 + s1;
    return doubledString.contains(s2);
}
```

### Time/Space Complexity

Same complexity as .contains() function. If .contains() is implemented using the [KMP algorithm](https://en.wikipedia.org/wiki/Knuth%E2%80%93Morris%E2%80%93Pratt_algorithm), then we will have

- Time Complexity: O(n)
- Space Complexity: O(1)

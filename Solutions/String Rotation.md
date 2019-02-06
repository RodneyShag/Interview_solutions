#### Solution

```java
boolean isRotation(String s1, String s2) {
    if (s1.length() != s2.length()) {
        return false;
    }
    String doubledString = s1 + s1;
    return doubledString.contains(s2);
}
```

#### Time/Space Complexity

- Same complexity as .contains() function

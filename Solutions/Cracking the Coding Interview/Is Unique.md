### Tips

Should ask interviewer if String is ASCII or Unicode (We assume ASCII)

### Solution

```java
boolean uniqueCharacters(String str) {
    final int NUM_ASCII_CHARS = 256;
    if (str.length() > NUM_ASCII_CHARS) {
        return false;
    }
    HashSet<Character> mySet = new HashSet(NUM_ASCII_CHARS);
    for (int i = 0; i < str.length(); i++) {
        if (mySet.contains(str.charAt(i))) {
            return false;
        } else {
            mySet.add(str.charAt(i));
        }
    }
    return true;
}
```

### Time/Space Complexity

- Time Complexity: O(1)
- Space Complexity: O(1)
- Checking `str.length() > 256` lowered our time complexity from O(n) to O(1)

### Solution to Follow-up Question

- Can do brute-force solution by comparing all pairs
- Time Complexity: O(1) since String is max 256 characters. Without this bound it would be O(n<sup>2</sup>)
- Space Complexity: O(1)

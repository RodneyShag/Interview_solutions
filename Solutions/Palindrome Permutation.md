#### Solution

```java
boolean palPerm(String str) {
    final int NUM_LOWERCASE_LETTERS = 26;
    str = str.toLowerCase().replaceAll("\\s", "");
    HashMap<Character, Integer> map = new HashMap<>(NUM_LOWERCASE_LETTERS);
    for (int i = 0; i < str.length(); i++) {
        Character ch = str.charAt(i);
        if (Character.isLetter(ch)) {
            map.merge(ch, 1, Integer::sum);
        }
    }

    //  Odd length strings: Can have at most 1 character an odd # of times
    // Even length strings: Can have either 0,2,4,6... number of odd characters.
    //                      Anything above 1 means not a palindrome.
    int oddCount = 0;
    for (Integer value : map.values()) {
        if (value % 2 != 0) {
            oddCount++;
        }
        if (oddCount > 1) {
            return false;
        }
    }
    return true;
}
```

#### Time/Space Complexity

- Time Complexity: O(n)
- Space Complexity: O(1)

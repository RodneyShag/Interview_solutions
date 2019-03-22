### Notes

- Create `HashMap` to match opening brackets with closing bracket.
- `ArrayDeque` is "likely to be faster than Stack when used as a stack" - [Java documentation](https://docs.oracle.com/javase/8/docs/api/java/util/ArrayDeque.html)

### Solution

```java
boolean isValid(String str) {
    HashMap<Character, Character> map = new HashMap<>();
    map.put('(', ')');
    map.put('[', ']');
    map.put('{', '}');

    if ((str.length() % 2) != 0) {
        return false; // odd length Strings are not balanced
    }        
    ArrayDeque<Character> deque = new ArrayDeque<>(); // use deque as a stack
    for (int i = 0; i < str.length(); i++) {
        Character ch = str.charAt(i);
        if (map.containsKey(ch)) {
            deque.push(ch);
        } else if (deque.isEmpty() || ch != map.get(deque.pop())) {
            return false;
        }
    }
    return deque.isEmpty();
}
```

### Time/Space Complexity

- Time Complexity: O(n)
- Space Complexity: O(n)

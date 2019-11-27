### Solution

```java
String superReducedString(String str) {
    // Iterate through String, creating final result in a Stack
    Stack<Character> stack = new Stack();
    for (int i = 0; i < str.length(); i++) {
        Character ch = str.charAt(i);
        if (!stack.isEmpty() && ch == stack.peek()) {
            stack.pop(); // since String has 2 adjacent equal characters
        } else {
            stack.push(ch);
        }
    }

    // Return final result
    if (stack.isEmpty()) {
        return "Empty String";
    } else {
        StringBuffer sb = new StringBuffer();
        for (char ch : stack) {
            sb.append(ch);
        }
        return sb.toString();
    }
}
```

### Notes

Can alternatively use an `ArrayDeque` instead of a `Stack`. Just make sure to iterate through it properly since iteration order is opposite that of a Stack.

### Time/Space Complexity

- Time Complexity: O(n)
- Space Complexity: O(n)

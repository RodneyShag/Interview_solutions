### Solution

```java
Stack<Integer> sort(Stack<Integer> stack) {
    Stack<Integer> helperStack = new Stack(); // can alternatively use ArrayDeque (it's faster)
    while (!stack.isEmpty()) {
        Integer curr = stack.pop(); // saving the top of the stack is one of the main tricks.
        while (!helperStack.isEmpty() && curr < helperStack.peek()) {
            stack.push(helperStack.pop());
        }
        helperStack.push(curr);
    }
    return helperStack;
}
```

### Time/Space Complexity

- Time Complexity: O(n<sup>2</sup>)
- Space Complexity: O(n)

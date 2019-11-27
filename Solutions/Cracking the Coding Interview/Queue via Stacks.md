### Algorithm

- `stack1` will accept input elements for `push()`
- `stack2` will output elements for `pop()`, `peek()`
- when trying to do a `pop()` or `peek()` on our queue, if `stack2` is empty, we will move all elements from `stack1` to `stack2`. This will reverse the order of the elements, giving us the correct order when we call `pop()` or `peek()` on our queue.

### Solution

```java
class QueueViaStacks<T> {
    private Stack<T> stack1 = new Stack();
    private Stack<T> stack2 = new Stack();

    public int size() {
        return stack1.size() + stack2.size();
    }

    public void add(T item) {
        stack1.push(item);
    }

    public T remove() {
        if (size() == 0) {
            return null;
        }
        if (stack2.isEmpty()) {
            shiftStacks();
        }
        return stack2.pop();
    }

    public T peek() {
        if (size() == 0) {
            return null;
        }
        if (stack2.isEmpty()) {
            shiftStacks();
        }
        return stack2.peek();
    }

    private void shiftStacks() {
        while (!stack1.isEmpty()) {
            T temp = stack1.pop();
            stack2.push(temp);
        }
    }
}
```

### Time/Space Complexity

-  Time Complexity: O(1) _amortized_ time for `push()`, `pop()`, `peek()`, `empty()`, as each element is only moved from `stack1` to `stack2` at most once.
- Space Complexity: O(1) for each element being put into our queue.

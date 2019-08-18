### Solution

```java
int multiply(int a, int b) {
    if (a == 0 || b == 0) {
        return 0;
    } else if (a < b) {
        return multiplyHelper(a, b);
    } else {
        return multiplyHelper(b, a);
    }
}

private int multiplyHelper(int smaller, int bigger) {
    if (smaller == 1) {
        return bigger;
    }

    int halfProd = multiplyHelper(smaller / 2, bigger);

    if (smaller % 2 == 0) {
        return halfProd + halfProd;
    } else {
        return halfProd + halfProd + bigger;
    }
}
```

### Time/Space Complexity

-  Time Complexity: O(log s) where s is the smaller of the 2 numbers
- Space Complexity: O(log s) due to recursion. This problem required us to code this function recursively. If we converted it to an iterative solution, it would be O(1) space.

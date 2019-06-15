### Main trick

Using `n % 10` and `n /= 10` to loop through digits of a number.

### Solution

```java
int findDigits(int num) {
    int count = 0;
    int n = num;
    while (n > 0) {
        int digit = n % 10;
        if (digit != 0 && num % digit == 0) {
            count++;
        }
        n /= 10;
    }
    return count;
}
```

### Time/Space Complexity

Regardless of how big our `int` is, the while loop will end in about ~10 iterations.

-  Time Complexity: O(1)
- Space Complexity: O(1)

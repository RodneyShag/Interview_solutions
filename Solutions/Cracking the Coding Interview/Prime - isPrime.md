### Solution

```java
boolean isPrime(int n) {
    if (n < 2) {
        return false;
    } else if (n == 2) {     // account for even numbers now, so that we can do i+=2 in loop below
        return true;
    } else if (n % 2 == 0) { // account for even numbers now, so that we can do i+=2 in loop below
        return false;
    }
    int sqrt = (int) Math.sqrt(n);
    for (int i = 3; i <= sqrt; i += 2) { // skips even numbers for faster results
        if (n % i == 0) {
            return false;
        }
    }
    return true;
}
```

### Time/Space Complexity

-  Time Complexity: O(n<sup>1/2</sup>)
- Space Complexity: O(1)

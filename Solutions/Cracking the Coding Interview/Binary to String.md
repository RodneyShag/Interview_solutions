### Solution

```java
String printBinary(double num) {
    final int MAX_CHARACTERS = 32;
    if (num >= 1 || num <= 0) {
        return "Error";
    }

    StringBuffer sb = new StringBuffer();
    sb.append(".");

    while (num > 0) {
        num *= 2;
        if (num >= 1) {
            sb.append(1); // automatically converts the int to a String
            num = num - 1;
        } else {
            sb.append(0);
        }
        if (sb.length() > MAX_CHARACTERS) {
            return "ERROR";
        }
    }

    return sb.toString();
}
```

### Time/Space Complexity

-  Time Complexity: O(1)
- Space Complexity: O(1)

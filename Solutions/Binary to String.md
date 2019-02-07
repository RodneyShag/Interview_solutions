#### Solution

```java
String printBinary(double num) {
    final int MAX_CHARACTERS = 32;
    if (num >= 1 || num <= 0) {
        return "ERROR";
    }

    StringBuffer binary = new StringBuffer();
    binary.append(".");

    while (num > 0) {
        num *= 2;
        if (num >= 1) {
            binary.append(1); // automatically converts the int to a String
            num = num - 1;
        } else {
            binary.append(0);
        }
        if (binary.length() > MAX_CHARACTERS) {
            return "ERROR";
        }
    }

    return binary.toString();
}
```

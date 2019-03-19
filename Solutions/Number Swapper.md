### Solution

```java
void swap1(int a, int b) {
    a = a - b;
    b = b + a;
    a = b - a;
    System.out.println("Swapped (Solution 1): a = " + a + "  b = " + b);
}

void swap2(int a, int b) {
    a = a ^ b;
    b = a ^ b;
    a = a ^ b;
    System.out.println("Swapped (Solution 2): a = " + a + "  b = " + b);
}
```

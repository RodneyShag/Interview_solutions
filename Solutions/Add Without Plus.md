#### Solution

```java
int add(int a, int b) {
    if (b == 0) {
        return a;
    }
    int sum = a ^ b;
    int carry = (a & b) << 1;
    return add(sum, carry);
}

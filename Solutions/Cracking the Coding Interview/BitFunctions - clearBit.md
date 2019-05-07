### Solution

```java
int clearBit(int num, int bit) {
    int mask = ~(1 << bit);
    return num & mask;
}
```

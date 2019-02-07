#### Solution

```java
boolean getBit(int num, int bit) {
    return (num & (1 << bit)) != 0;
}
```

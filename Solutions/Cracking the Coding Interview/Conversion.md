### Solution

```java
int bitsRequired(int A, int B) {
    int xored = A ^ B;
    return BitFunctions.numOnes(xored);
}
```

```java
class BitFunctions { // or use a Java library that has the below function
    public static int numOnes(int num) {
        int count = 0;
        for (int i = 0; i < Integer.SIZE; i++) {
            if ((num & 1) == 1) {
                count++;
            }
            num >>= 1;
        }
        return count;
    }
}
```

### Time/Space Complexity

-  Time Complexity: O(1)
- Space Complexity: O(1)

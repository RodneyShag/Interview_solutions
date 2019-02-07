#### Optionally implement your own BitSet

```java

public class MyBitSet {
    private static final int BITS_IN_INT = Integer.BYTES * 8;
    private int[] bitset;

    public MyBitSet(int size) throws NegativeArraySizeException {
        if (size < 0) {
            throw new NegativeArraySizeException();
        }
        bitset = new int[size / BITS_IN_INT + 1];
    }

    /* I needed this constructor for 10.3. Long enables me to make HUGE arrays */
    public MyBitSet(long size) throws NegativeArraySizeException {
        if (size < 0) {
            throw new NegativeArraySizeException();
        }
        bitset = new int[(int) (size / BITS_IN_INT) + 1];
    }

    public boolean get(int pos) throws IndexOutOfBoundsException {
        if (pos < 0) {
            throw new IndexOutOfBoundsException();
        }
        int wordNumber = pos / BITS_IN_INT;
        int bitNumber = pos % BITS_IN_INT;
        if (wordNumber >= bitset.length) {
            throw new IndexOutOfBoundsException();
        }
        return (bitset[wordNumber] & (1 << bitNumber)) != 0;
    }

    public void set(int pos) throws IndexOutOfBoundsException {
        if (pos < 0) {
            throw new IndexOutOfBoundsException();
        }
        int wordNumber = pos / BITS_IN_INT;
        int bitNumber = pos % BITS_IN_INT;
        if (wordNumber >= bitset.length) {
            throw new IndexOutOfBoundsException();
        }
        bitset[wordNumber] |= (1 << bitNumber);
    }

    public int size() {
        return bitset.length / BITS_IN_INT;
    }
}
```

#### Solution

```java
void findNumber(int[] input) {
    final long ONE_GB = 8000000000L;

    // My implementation of BitSet has constructor that takes a long (java.util.BitSet doesn't)
    MyBitSet bitset = new MyBitSet(ONE_GB);

    /* Initialize bitfield to represent numbers we already have */
    for (int num : input) {
        bitset.set(num);
    }

    /* Find first bit that is 0 and print corresponding number */
    for (int i = 0; i < bitset.size(); i++) {
        boolean bit = bitset.get(i);
        if (!bit) {
            System.out.println("(Solution 1) First missing number = " + i);
            break;
        }
    }
}
```

#### Follow-up Solution

```java
void findNumber2(int[] input) {
    int partitionSize = (int) Math.pow(2, 18);
    int numBlocks = (int) Math.pow(2, 12);
    MyBitSet bitset = new MyBitSet(partitionSize); // this takes up 2^18 bits
    int[] blocks = new int[numBlocks]; // this takes up 2^12 * (2^5 bits in int) = 2^17 bits

    /* Set up each block to have the count of numbers in that range */
    for (int num : input) {
        blocks[num / partitionSize]++;
    }

    /* Find 1st block that's missing a number */
    int lowerBound = -1;
    for (int i = 0; i < numBlocks; i++) {
        if (blocks[i] < partitionSize) {
            lowerBound = i * partitionSize;
            break;
        }
    }

    // The next 2 parts are very similar to part A of this problem.

    /* Do 2nd pass of file of numbers and record them into bitset */
    // scan = new Scanner(new FileReader("src/chapter10/numbers"));
    for (int num : input) {
        if (num >= lowerBound && num < lowerBound + partitionSize) {
            bitset.set(num - lowerBound);
        }
    }

    /* Loop through bitset and print the 1st missing number */
    for (int i = 0; i < bitset.size(); i++) {
        boolean bit = bitset.get(i);
        if (!bit) {
            System.out.println("(Solution 2) First missing number = " + i);
            break;
        }
    }
}
```

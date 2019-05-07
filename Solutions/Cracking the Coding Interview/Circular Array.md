### Solution

```java
class CircularArray<T> {
    private int head = 0;
    private T[] items; // I don't use an ArrayList since I want a fixed size array that doesn't grow

    public CircularArray(int size) {
        items = (T[]) new Object[size]; // since we cannot create an array of a generic type
    }

    public T get(int index) {
        if (index < 0 || index >= items.length) {
            throw new IndexOutOfBoundsException();
        }
        return items[convert(index)];
    }

    public void set(int index, T item) throws IndexOutOfBoundsException {
        if (index < 0 || index >= items.length) {
            throw new IndexOutOfBoundsException();
        }
        items[convert(index)] = item;
    }

    private int convert(int index) {
        if (index < 0) {
            index += items.length;
        }
        return (head + index) % items.length;
    }

    public void rotate(int shiftRight) {
        head = (head + shiftRight) % items.length;
    }
}
```

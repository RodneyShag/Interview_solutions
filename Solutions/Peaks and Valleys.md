#### Algorithm

Look at groups of 3 and put the "valleys" in the right place. This will also make the "peaks" fall in the right place.


#### Solution

```java
void sortValleyPeak(int[] array) {
    for (int i = 1; i < array.length; i += 2) {
        if (array[i - 1] < array[i]) {
            swap(array, i - 1, i);
        }
        if (i + 1 < array.length && array[i + 1] < array[i]) {
            swap(array, i + 1, i);
        }
    }
}

private void swap(int[] array, int left, int right) {
    int temp = array[left];
    array[left] = array[right];
    array[right] = temp;
}
```

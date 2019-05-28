### Algorithm

- To achieve O(log n) runtime, we will use a variation of binary search.
- In every iteration of the while loop, we will compare the middle of the array to the left and right endpoints.
- If `array[mid] - array[start] < array[end] - array[mid]`, then we know the missing element is in the right half, otherwise, it's in the left half.
- Edge case: Since we used `mid = (start + end) / 2`, we made `mid` be closer to the left of array instead of the right for even-length arrays. So if `array[mid] - array[start] == array[end] - array[mid]`, the missing element must be on the left side since there are fewer elements on that side.
  - Example: [1,5,7,9]. `mid` is 5, and missing element must be to the left.

### Solution

Function below assumes `array` is a sorted arithmetic sequence of length 3 or more, with exactly 1 missing element within the first and last elements (exclusive) of the array.

```java
public class Solution {
    public static int findElement(int[] array) {
        int start = 0;
        int end = array.length - 1;

        while (true) {
            if (start + 1 == end) {
                return (array[start] + array[end]) / 2; // base case
            }
            int mid = (start + end) / 2;
            if (array[mid] - array[start] < array[end] - array[mid]) {
                start = mid;
            } else {
                end = mid;
            }
        }
    }

    public static void main(String[] args) {
        System.out.println(findElement(new int[]{1, 3, 5, 9})); // missing 7
        System.out.println(findElement(new int[]{1, 5, 7, 9})); // missing 3
        System.out.println(findElement(new int[]{1, 3, 7, 9})); // missing 5
        System.out.println(findElement(new int[]{1, 3, 7, 9, 11})); // missing 5
        System.out.println(findElement(new int[]{-11, -9, -7, -3, -1})); // missing -5
    }
}
```


### Time Complexity

- Time Complexity: O(log n)
- Space Complexity: O(1)


### Compiler

- To execute this code, just copy paste it to [this online Java compiler](https://www.tutorialspoint.com/compile_java_online.php)

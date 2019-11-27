### Algorithm

- A `HashMap` will let us keep track of the count of each number.
- An `ArrayDeque` will let us keep track of the "contiguous subarray" (sliding window) of size `m`

### Notes

HackerRank has a strange input format where we have to read the input from standard input. Ignore that part of the code.
### Solution

```java
public class test {
    public static void main(String[] args) {
        Map<Integer, Integer> map = new HashMap();
        Deque<Integer> deque = new ArrayDeque();

        Scanner scan = new Scanner(System.in);
        int n = scan.nextInt();
        int m = scan.nextInt();
        int max = 0;

        for (int i = 0; i < n; i++) {
            // Remove old value (if necessary)
            if (i >= m) {
                int old = deque.removeFirst();
                if (map.get(old) == 1) {
                    map.remove(old);
                } else {
                    map.merge(old, -1, Integer::sum);
                }
            }

            // Add new value
            int num = scan.nextInt();
            deque.addLast(num);
            map.merge(num, 1, Integer::sum);

            max = Math.max(max, map.size());

            // If all integers are unique, we have found our largest
            // possible answer, so we can break out of loop
            if (max == m) {
                break;
            }
        }

        scan.close();
        System.out.println(max);
    }
}
```

### Time/Space Complexity

- Time Complexity: O(n)
- Space Complexity: O(n)

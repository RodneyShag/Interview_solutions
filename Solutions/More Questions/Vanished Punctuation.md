### Algorithm

- Let `valid(i)` be a function that determines if a String from start to index `i` (exclusive) is valid document.
- For `i = 0`, we have the empty string, and this qualifies as a valid document, giving us __true__ as our base case.
- For a String up to a given index, it is a valid document if we can split the String into 2 parts where
    1. The 1st part is a valid document. (which we can check recursively)
    1. The 2nd part is a valid word.
- For the above step, we will split the string up in `i` possible locations (where `0 <= i < index`) and see if any create a valid document.

### Solution

```java
public class Solution {
    public static void main(String[] args) {
        String str = "itwasthebestoftimes";
        HashSet<String> dict = new HashSet<>(Arrays.asList("it", "was", "the", "best", "of", "times"));
        System.out.println(isValid(str, dict));
    }

    public static boolean isValid(String str, HashSet<String> dict) {
        Map<Integer, Boolean> cache = new HashMap<>();
        cache.put(0, true); // base case
        return isValid(str, dict, str.length(), cache);
    }

    private static boolean isValid(String str, HashSet<String> dict, int index, Map<Integer, Boolean> cache) {
        Integer key = index;
        if (cache.containsKey(key)) {
            return cache.get(key);
        }
        boolean result = false;
        for (int i = 0; i < index; i++) {
            if (isValid(str, dict, i, cache) && dict.contains(str.substring(i, index))) {
                result = true;
                break;
            }
        }
        cache.put(key, result);
        return result;
    }
}
```

### Time/Space Complexity

- Time Complexity: O(n^2)
- Space Complexity: O( n)

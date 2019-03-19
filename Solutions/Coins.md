### Tips

- The first 1/2 page of "Cracking the Coding Interview" is a great thing to explain during an interview.
- This is a dynamic programming question. Solve it recursively using a cache.

### Solution

```java
public class Coins {
    long makeChange(int n) {
        HashMap<String, Long> cache = new HashMap<>();
        return makeChange(n, 25, cache);
    }

    private long makeChange(int n, int denom, HashMap<String, Long> cache) {
        String key = n + "," + denom;
        if (cache.containsKey(key)) {
            return cache.get(key);
        }
        int nextDenom = 0;
        switch (denom) {
            case 25:
                nextDenom = 10;
                break;
            case 10:
                nextDenom = 5;
                break;
            case 5:
                nextDenom = 1;
                break;
            case 1:
                cache.put(key, 1L);
                return 1;
            default:
                return 0; // something wen't wrong if we get here.
        }

        /* The main algorithm */
        long ways = 0;
        for (int i = 0; i <= n; i += denom) { // notice it's: i <= n
            ways += makeChange(n - i, nextDenom, cache);
        }
        cache.put(key, ways);
        return ways;
    }
}
```

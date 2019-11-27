### Algorithm

- count `directHits` first
- put all non-hit characters into a `Map<Character, Integer>`
- count `pseudoHits`.

### Solution

```java
class Result {
    int directHits = 0;
    int pseudoHits = 0;
}
```

```java
Result estimate(String guess, String solution) {
    if (guess.length() != solution.length()) {
        return null;
    }
    guess    = guess.toLowerCase();
    solution = solution.toLowerCase();

    Result result = new Result();
    Map<Character, Integer> colorMap = new HashMap();

    // Count direct hits. Save other colors in HashMap for later.
    for (int i = 0; i < solution.length(); i++) {
        char solChar = solution.charAt(i);
        char guessChar = guess.charAt(i);
        if (solChar == guessChar) { // direct "hit"
            result.directHits++;
        } else {
            colorMap.merge(solChar, 1, Integer::sum);
        }
    }

    // Count pseudo hits in HashMap
    for (int i = 0; i < guess.length(); i++) {
        char solChar   = solution.charAt(i);
        char guessChar = guess.charAt(i);
        if (solChar == guessChar) {
            continue; // this was already counted as a direct hit
        }
        if (colorMap.containsKey(guessChar)) {
            int count = colorMap.get(guessChar);
            if (count > 0) {
                result.pseudoHits++;
                colorMap.put(guessChar, count - 1);
            }
        }
    }
    return result;
}
```

### Time/Space Complexity

-  Time Complexity: O(n)
- Space Complexity: O(n)

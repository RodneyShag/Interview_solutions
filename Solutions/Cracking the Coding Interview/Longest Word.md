### Algorithm

1. Sort Array in order by string length.
1. Save original `String[]` in a `HashMap<String, Boolean>` to save words for fast lookup. Also use this to cache results.
1. A word must be built of OTHER words. `isOriginalWord` flag helps us do this.

### Solution

```java
String longestWord(String[] words) {
    Arrays.sort(words, (s1, s2) -> s2.length() - s1.length()); // sorting backwards to put longer words in front
    Map<String, Boolean> map = makeMap(words);

    for (String word : words) {
        if (canBuildWord(word, true, map)) {
            return word;
        }
    }
    return null;
}

private Map<String, Boolean> makeMap(String[] words) {
    Map<String, Boolean> map = new HashMap();
    for (String word : words) {
        map.put(word, true);
    }
    return map;
}

private boolean canBuildWord(String word, boolean isOriginalWord, Map<String, Boolean> cache) {
    if (!isOriginalWord && cache.containsKey(word)) {
        return cache.get(word);
    }
    for (int i = 1; i < word.length(); i++) {
        String left = word.substring(0, i);
        String right = word.substring(i);
        if (canBuildWord(left, false, cache) && canBuildWord(right, false, cache)) {
            cache.put(word, true);
            return true;
        }
    }
    cache.put(word, false);
    return false;
}
```

### Time Complexity

- Sorting `n` words takes `O(n log n)`. If we include String lengths in there, it becomes `O(ns log(ns))`
- `canBuildWord()` is `O(s)` where `s` is length of longest String.
- `canBuildWord()` is called `O(n)` where `n` is number of words.
- Total time complexity is `O(ns log(ns))`. We can optionally omit `s` and just represent the runtime as `O(n log n)`

### Space Complexity

`O(ns)` to store `n` words of max length `s` in our `Map`. We can optionally omit `s` and just represent the space complexity as `O(n)`

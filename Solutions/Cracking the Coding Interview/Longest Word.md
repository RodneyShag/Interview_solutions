### Algorithm

1. Sort Array in order by string length.
1. Save original `String[]` in a `HashMap<String, Boolean>` to save words for fast lookup. Also use this to cache results.
1. A word must be built of OTHER words. `isOriginalWord` flag helps us do this.

### Solution

```java
String longestWord(String[] words) {
    Arrays.sort(words, (s1, s2) -> s2.length() - s1.length()); // sorting backwards to put longer words in front.
    Map<String, Boolean> map = makeMap(words);

    for (String word : words) {
        if (canBuildWord(word, true, map)) {
            return word;
        }
    }
    return null;
}

private Map<String, Boolean> makeMap(String[] words) {
    Map<String, Boolean> map = new HashMap<>();
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

### Algorithm

1. Sort Array in order by string length.
1. Save original `String[]` in a `HashMap<String, Boolean>` to save words for fast lookup. Also use this to cache results.
1. A word must be built of OTHER words. `isOriginalWord` flag helps us do this.

### Solution

```java
class LengthComparator implements Comparator<String> {
    @Override
    public int compare(String s1, String s2) {
        return s2.length() - s1.length(); // sorting backwards to put longer words in front.
    }
}
```

```java
String longestWord(String[] words) {
    Arrays.sort(words, new LengthComparator()); // we want to search longest words first
    HashMap<String, Boolean> map = makeMap(words);

    for (String word : words) {
        if (canBuildWord(word, true, map)) {
            return word;
        }
    }
    return null;
}

private static HashMap<String, Boolean> makeMap(String[] words) {
    HashMap<String, Boolean> map = new HashMap<>();
    for (String word : words) {
        map.put(word, true);
    }
    return map;
}

private static boolean canBuildWord(String word, boolean isOriginalWord, HashMap<String, Boolean> cache) {
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

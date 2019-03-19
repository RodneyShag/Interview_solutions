### Solution

```java
void checkMagazine(String[] magazine, String[] note) {
    HashMap<String, Integer> usableWords = makeMap(magazine);
    for (int i = 0; i < note.length; i++) {
        if (usableWords.containsKey(note[i]) && usableWords.get(note[i]) > 0) {
            usableWords.merge(note[i], -1, Integer::sum); // uses the word
        } else {
            System.out.println("No");
            return;
        }
    }
    System.out.println("Yes");
}

/* Creates and returns a HashMap out of an array of Strings */
private HashMap<String, Integer> makeMap(String [] words) {
    HashMap<String, Integer> map = new HashMap<>();
    for (int i = 0; i < words.length; i++) {
        map.merge(words[i], 1, Integer::sum);
    }
    return map;
}
```

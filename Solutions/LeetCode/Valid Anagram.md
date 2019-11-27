### Algorithm

- Do a quick check on string lengths. If the lengths differ, the strings can't be anagrams
- Save `String s` as `HashMap` of character counts
- For `String t`, see if it can be made up of the characters of the previous `HashMap`

### Solution

```java
class Solution {
    public boolean isAnagram(String s, String t) {
        if (s.length() != t.length()) {
            return false;
        }
        Map<Character, Integer> map = new HashMap();
        for (int i = 0; i < s.length(); i++) {
            char ch = s.charAt(i);
            map.merge(ch, 1, Integer::sum);
        }
        for (int i = 0; i < t.length(); i++) {
            char ch = t.charAt(i);
            if (!map.containsKey(ch) || map.get(ch) == 0) {
                return false;
            }
            map.merge(ch, -1, Integer::sum);
        }
        return true;
    }
}
```

### Time/Space Complexity

-  Time Complexity: O(n)
- Space Complexity: O(1), since our HashMap has a maximum size corresponding either to 256 ASCII characters, or to about 1 million Unicode characters.

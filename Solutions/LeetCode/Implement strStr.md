### Algorithm

- TBA

### Solution

```java
class Solution {
  // computes Longest Prefix-Suffix (LPS) array
  private int[] computeLPS(String str) {
    int[] lps = new int[str.length()];
    lps[0] = 0;
    int i = 1; // always walks forward
    int j = 0; // tracks prefix that matches suffix

    while (i < str.length()) {
      if (str.charAt(i) == str.charAt(j)) {
        j++;
        lps[i] = j;
        i++;
      } else { // mismatch
        if (j == 0) { // go onto next character in string
          lps[i] = 0;
          i++;
        } else { // backtrack "len" to check our prefix, do not increment i.
          j = lps[j-1];
        }
      }
    }
    return lps;
  }

  int strStr(String haystack, String needle) {
      if (needle == null || needle.isEmpty()) {
          return 0;
      } else if (haystack == null || haystack.isEmpty()) {
          return -1;
      }

      int[] lps = computeLPS(needle);
      int i = 0;
      int j = 0;

      while (i < haystack.length()) {
          if (needle.charAt(j) == haystack.charAt(i)) {
              i++;
              j++;
              if (j == needle.length()) {
                  return i - j;
              }
          } else {
              if (j == 0) {
                  i++;
              } else {
                 j = lps[j - 1];
              }
          }
      }


      return -1; // did not find needle
  }
}
```

### Time/Space Complexity

- Time Complexity: O(m+n)
- Space Complexity: O(m)

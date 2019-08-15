# Solution 1 - Recursive

### Algorithm

Let SCS(i, j) be the length of the Shortest Common Supersequence (SCS) of X[1...i] and Y[1...j]. Notice we are representing X, Y as 1-indexed instead of 0-indexed, so that 0 can represent an empty array.

```
SCS(i,j) =

i                                      if j == 0
j                                      if i == 0
SCS(i - 1, j - 1) + 1                  if X[i] == Y[j]
min(SCS(i - 1, j), SCS(i, j - 1)) + 1  otherwise
```

- __Fact 1, 2__ - If either i or j is 0, then we are asking for the SCS of a string and the empty string, so the SCS is the length of the nonempty string itself (depicted in first 2 rules above).
- __Fact 3__ - Otherwise, if the last characters match (X[i] == Y[j]), then the SCS is the SCS of X[1 ... i − 1] and Y [1 ... j − 1] with the last character appended.
- __Fact 4__ - If the last characters do not match, then the SCS is obtained by either adding X[i] to the SCS of X[1 ... i − 1] and Y [1 ... j], or by adding Y[j] to the SCS of X[1 ... i] and Y [1 ... j − 1].

### Code

```java
public class Solution {
    public static int shortestCommonSubsequence(char[] X, char[] Y) {
        // use X.length instead of X.length - 1, since X, Y are 1-indexed in our definition, 0-indexed in code
        return scs(X, Y, X.length, Y.length, new HashMap<String, Integer>());
    }

    private static int scs(char[] X, char[] Y, int i, int j, Map<String, Integer> cache) {
        String key = i + " " + j;
        if (cache.containsKey(key)) {
            return cache.get(key);
        }
        int result;
        if (i == 0) {
            result = j;
        } else if (j == 0) {
            result = i;
        } else if (X[i - 1] == Y[j - 1]) { // X, Y are 1-indexed in our definition, 0-indexed in code
            result = scs(X, Y, i - 1, j - 1, cache) + 1;
        } else {
            result = Math.min(scs(X, Y, i - 1, j, cache), scs(X, Y, i, j - 1, cache)) + 1;
        }
        cache.put(key, result);
        return result;
    }

    public static void main(String[] args) {
        System.out.println(SCS(new char[]{'a', 'b', 'd', 'c'}, new char[]{'b', 'a', 'b', 'e', 'd'}));
        // Shortest Common Supersequence is babedc, which is of length 6.
    }
}
```

### Time/Space Complexity

- Time Complexity: O(m * n)
- Space Complexity: O(m * n)


# Solution 2 - Iterative

### Algorithm

- Use same recursive definition as above.
- We can use Dynamic Programming to fill a 2-D array for every `i`, `j`.
- Instead of creating an array of size `m` by `n`, we will make an array of size `m + 1` by `n + 1`. This trick helps us write more concise code. scs[1][1] will represent X[0], Y[0].

### Code

```java
public class Solution {
    public static int SCS(char[] X, char[] Y) {
        int m = X.length;
        int n = Y.length;
        int[][] scs = new int[m + 1][n + 1];
        for (int i = 0; i <= m; i++) {
            for (int j = 0; j <= n; j++) {
                if (i == 0) {
                    scs[i][j] = j;
                } else if (j == 0) {
                    scs[i][j] = i;
                } else if (X[i - 1] == Y[j - 1]) { // X, Y are 1-indexed in our definition, 0-indexed in code
                    scs[i][j] = scs[i - 1][j - 1] + 1;
                } else {
                    scs[i][j] = Math.min(scs[i - 1][j], scs[i][j - 1]) + 1;
                }
            }
        }
        return scs[m][n];
    }

    public static void main(String[] args) {
        System.out.println(SCS(new char[]{'a', 'b', 'd', 'c'}, new char[]{'b', 'a', 'b', 'e', 'd'}));
        // Shortest Common Supersequence is babedc, which is of length 6.
    }
}
```

### Time/Space Complexity

- Time Complexity: O(m * n)
- Space Complexity: O(m * n)


# Solution 3 - Iterative, with space optimization

The above solution is definitely satisfactory in an interview. This next solution builds on Solution 2, but is very tricky.

### Algorithm

- We can reduce the space complexity to `O(n)`, by noticing that `scs[i][j]` only depends on the current row `scs[i][j - 1]`, and the row above it (`scs[i + 1][j - 1]` and `scs[i + 1][j]`). So instead of storing an entire 2-D array of data, a 1-D array of data will be enough. Mentioning this will score bonus points in an interview.
- Coding it is tricky. Now, from `scs[j]`, to get the value:
  - `scs[i - 1][j]` is "up". It becomes `scs[j]`
  - `scs[i][j - 1]` is "left". It becomes `scs[j - 1]`
  - `scs[i - 1][j - 1]` is "up-left". It becomes `scs[j - 1]` __before__ we overwrite it, so we preserve that value across iterations of the inner for loop. This is done using 2 variables: `pre` and `tmp` (see code below)

### Code

```java
public class Solution {
    public static int SCS(char[] X, char[] Y) {
        int m = X.length;
        int n = Y.length;
        int[] scs = new int[n + 1];
        int pre = 0;
        for (int i = 0; i <= m; i++) {
            for (int j = 0; j <= n; j++) {
                int tmp = scs[j];
                if (i == 0) {
                    scs[j] = j;
                } else if (j == 0) {
                    scs[j] = i;
                } else if (X[i - 1] == Y[j - 1]) { // X, Y are 1-indexed in our definition, 0-indexed in code
                    scs[j] = pre + 1;
                } else {
                    scs[j] = Math.min(scs[j], scs[j - 1]) + 1;
                }
                pre = tmp;
            }
        }
        return scs[n];
    }

    public static void main(String[] args) {
        System.out.println(SCS(new char[]{'a', 'b', 'd', 'c'}, new char[]{'b', 'a', 'b', 'e', 'd'}));
        // Shortest Common Supersequence is babedc, which is of length 6.
    }
}
```

### Time/Space Complexity

  - Time Complexity: O(m * n)
  - Space Complexity: O(m)

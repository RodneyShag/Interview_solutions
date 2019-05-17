### Algorithm

Let SCS(i, j) be the length of the Shortest Common Supersequence (SCS) of X[1...i] and Y[1...j]. Notice we are representing X, Y as 1-indexed instead of 0-indexed, so that 0 can represent an empty array.

```
SCS(i,j) =

i                                      if j == 0
j                                      if i == 0
1 + SCS(i - 1, j - 1)                  if X[i] == Y[j]
1 + min(SCS(i - 1, j), SCS(i, j - 1))  otherwise
```

- __Fact 1, 2__ - If either i or j is 0, then we are asking for the SCS of a string and the empty string, so the SCS is the length of the nonempty string itself (depicted in first 2 rules above).
- __Fact 3__ - Otherwise, if the last characters match (X[i] == Y[j]), then the SCS is the SCS of X[1 ... i − 1] and Y [1 ... j − 1] with the last character appended.
- __Fact 4___ - If the last characters do not match, then the SCS is obtained by either adding X[i] to the SCS of X[1 ... i − 1] and Y [1 ... j], or by adding Y[j] to the SCS of X[1 ... i] and Y [1 ... j − 1].


- We can use Dynamic Programming to fill a 2-D array for every `i`, `j`.
- Instead of creating an array of size `m` by `n`, we will make an array of size `m+1` by `n+1`. This trick helps us write more concise code. scs[1][1] will represent X[0], Y[0].

### Solution

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
                    scs[i][j] = 1 + scs[i - 1][j - 1];
                } else {
                    scs[i][j] = 1 + Math.min(scs[i - 1][j], scs[i][j - 1]);
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

### Compiler

- To execute this code, just copy paste it to [this online Java compiler](https://www.tutorialspoint.com/compile_java_online.php)

This problem is similar to [Implement Trie (Prefix Tree)](https://leetcode.com/problems/implement-trie-prefix-tree/) in LeetCode. The difference is that this question asks: "Given a prefix, return the __number__ of words that match that prefix."

### Solution

Code below is based loosely on tutorial video in this HackerRank problem

```java
class TrieNode {
    private Map<Character, TrieNode> children = new HashMap();
    public int size = 0; // this was the main trick to decrease runtime to pass tests.

    public void putChildIfAbsent(char ch) {
        children.putIfAbsent(ch, new TrieNode());
    }

    public TrieNode getChild(char ch) {
        return children.get(ch);
    }
}
```

```java
class Trie {
    TrieNode root = new TrieNode();

    public void add(String str) {
        TrieNode curr = root;
        for (char ch : str.toCharArray()) {
            curr.putChildIfAbsent(ch);
            curr = curr.getChild(ch);
            curr.size++;
        }
    }

    public int find(String prefix) {
        TrieNode curr = root;

        for (char ch : prefix.toCharArray()) {
            curr = curr.getChild(ch);
            if (curr == null) {
                return 0;
            }
        }
        return curr.size;
    }
}
```

### Time/Space Complexity

Let `n` be the length of a word. For `add()`, we have:

-  Time Complexity: O(n)
- Space Complexity: O(n)

For `find()` we have:

-  Time Complexity: O(n)
- Space Complexity: O(1)

### Provided code

```java
class SinglyLinkedListNode {
   int data;
   SinglyLinkedListNode next;
}
```

### Solution

```java
void reversePrint(SinglyLinkedListNode n) {
    if (n != null) {
        reversePrint(n.next);
        System.out.println(n.data);
    }
}
```

### Time/Space Complexity

- Time Complexity: O(n)
- Space Complexity: O(n) due to recursion

We _could_ improve the space complexity by using a more complex algorithm:

1. [Reverse list](https://github.com/RodneyShag/Interview_solutions/blob/master/Solutions/LeetCode/Reverse%20Linked%20List.md) in O(n) time, O(1) space
1. Loop through list and print elements in O(n) time, O(1) space
1. Re-reverse list in O(n) time, O(1) space

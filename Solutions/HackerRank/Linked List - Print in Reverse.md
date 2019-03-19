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

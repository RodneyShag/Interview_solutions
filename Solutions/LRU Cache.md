### Notes

- Excellent explanation in Cracking the Coding Interview, 6th Edition solutions
- __Why have our Node contain both key and value?__
 Answer: Because when we remove from end of Linked List, the Node's key is used to find the Node in the HashMap (to remove the node there as well)

### Solution

```java
class Node {
	  int key;
    String value;
    Node next;
    Node prev;

    public Node(int k, String v) {
    	key = k;
        value = v;
        next = null;
        prev = null;
    }
}

```

```java
class DoublyLinkedList {
    private Node head = null;
    private Node tail = null;

    public void addFirst(Node n) {
        if (head == null) {
            head = n;
            tail = n;
        } else {
        	n.prev = null;
            n.next = head;
            head.prev = n;
            head = n;
        }
    }

    public void remove(Node n) { // Assumes "Node n" is in this list
    	if (n == null) {
    		return;
    	}
    	if (n.prev != null) {
    		n.prev.next = n.next;
    	}
    	if (n.next != null) {
    		n.next.prev = n.prev;
    	}
    	if (n == head) {
    		head = n.next;
    	}
    	if (n == tail) {
    		tail = n.prev;
    	}
    }

    public void updateFreshness(Node n) { // Assumes "Node n" is in this list
    	remove(n);
        addFirst(n);
    }

    public Node getHead() {
    	return head;
    }

    public Node getTail() {
    	return tail;
    }
}
```

```java
class LRUCache {
    private int maxSize;
    private Map<Integer, Node> map; // gives us O(1)-time access to Nodes
    private DoublyLinkedList dll;   // used to keep track of "freshness" of Nodes

    public LRUCache(int maxSize) {
        this.maxSize = maxSize;
        map = new HashMap<>();
        dll = new DoublyLinkedList();
    }

    public void add(int key, String value) {
    	remove(key); // If key already exists, we will overwrite it.
    	if (map.size() == maxSize) {
    		remove(dll.getTail().key);
        }
    	Node n = new Node(key, value);
        dll.addFirst(n);
        map.put(key, n);
    }

    public void remove(int key) {
    	Node n = map.get(key);
        dll.remove(n);
        map.remove(key);
    }

    public String getValue(int key) {
    	Node n = map.get(key);
    	if (n == null) {
    		return null;
    	}
    	if (n != dll.getHead()) {
    	    dll.updateFreshness(n);
    	}
        return n.value;
    }
}
```

### Time/Space Complexity

#### Time Complexity
- `add()`is O(1) time
- `getValue()` is O(1) time
- `remove()` is O(1) time

#### Space Complexity
- Depends on cache size. Can make it as big as we want.

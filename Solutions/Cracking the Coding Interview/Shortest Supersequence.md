### Algorithm

1. For each integer in smaller array, create a list (or `Deque`) of its positions in larger list.

```
arrayA = [1 5 9]
arrayB = [7 5 9 9 2 1 3 5 7 9 1 1 5 8 8 9 7]

create HashMap<Integer, Deque<HeapNode>> of:

 key    [value, index]
  1 --> [1, 5] [1, 10] [1, 11]
  5 --> [5, 1] [5, 7] [5, 12]
  9 --> [9, 2] [9, 3] [9, 9] [9, 15]
```

2. Put head of each `Deque` into a `minHeap` and save `[min, max] Range`. The `[min, max]` range in the `minHeap` is always a solution range (although it may be too large).

```
Our minHeap:

[value, index]
[1, 5]
[5, 1]
[9, 2]

min = index 1
max = index 5
Range = [index 1, index 5]
```

3. Keep removing element in `minHeap` with minimum index and replace it with first element from list it came from. Stop when 1 of the lists is empty. After every replacement, we have a valid solution range (although it may be too large).

```
Our minHeap:

[value, index]
[1 5] --> [1 5] --> [1 5] --> [1 5] ==> [1 10]
[5 1] ==> [5 7] --> [5 7] --> [5 7] --> [5 7] ... and so on
[9 2] --> [9 2] ==> [9 3] ==> [9 9] --> [9 9]
Range     Range     Range     Range     Range
[1 5]     [2 7]     [3 7]     [5 9]     [7 10]
```

where [7, 10] is the best range
### Solution

```java
class HeapNode {
    int value; // saved so we know which deque this HeapNode came from
    int index; // index in arrayB

    HeapNode(int listID, int pos) {
        this.value = listID;
        this.index = pos;
    }
}
```

```java
class Range {
    Integer min;
    Integer max;

    Range(int min, int max) {
        this.min = min;
        this.max = max;
    }

    Range(Range other) {
        min = other.min;
        max = other.max;
    }

    void setRange(Range other) {
        min = other.min;
        max = other.max;
    }

    boolean isShorterThan(Range other) {
        return size() < other.size();
    }

    int size() {
        return max - min + 1;
    }
}
```

```java
Range shortest(int[] arrayA, int[] arrayB) {
    Map<Integer, Deque<HeapNode>> map = makeLists(arrayA, arrayB);
    return getSmallestRange(map);
}

// For each integer in smaller array, create a list of its positions in larger list
private Map<Integer, Deque<HeapNode>> makeLists(int[] arrayA, int[] arrayB) {
    Map<Integer, Deque<HeapNode>> map = new HashMap<>();
    for (int num : arrayA) {
        map.putIfAbsent(num, new ArrayDeque<>());
    }
    for (int i = 0; i < arrayB.length; i++) {
        if (map.containsKey(arrayB[i])) {
            Deque<HeapNode> deque = map.get(arrayB[i]);
            HeapNode node = new HeapNode(arrayB[i], i);
            deque.addLast(node);
        }
    }
    return map;
}

private Range getSmallestRange(Map<Integer, Deque<HeapNode>> map) {
    Queue<HeapNode> minHeap = new PriorityQueue<>((hn1, hn2) -> hn1.index - hn2.index);

    Range currRange = new Range(Integer.MAX_VALUE, Integer.MIN_VALUE);

    // - Put head of each list into a `minHeap`, and save [min, max] Range.
    // - The [min, max] range in the `minHeap` is always a
    //   solution range (although it may be too large).
    // - Tricky implementation: Update `max` when placing into minHeap.
    //   Update `min` when removing from minHeap.
    for (Deque<HeapNode> deque : map.values()) {
        HeapNode node = deque.removeFirst();
        currRange.max = Math.max(currRange.max, node.index);
        minHeap.add(node);
    }
    currRange.min = minHeap.peek().index;
    Range bestRange = new Range(currRange);

    // - Keep removing element in `minHeap` with minimum index and replace it
    //   with first element from list it came from. Stop when 1 of the lists is empty.
    // - After every replacement, we have a valid solution range (although it
    //   may be too large).
    while (true) {
        // Replace element
        HeapNode node = minHeap.remove();
        Deque<HeapNode> deque = map.get(node.value);
        if (deque.isEmpty()) {
            break;
        }
        HeapNode nodeToAdd = deque.removeFirst();
        minHeap.add(nodeToAdd);

        // Update ranges
        currRange.min = minHeap.peek().index;
        currRange.max = Math.max(currRange.max, nodeToAdd.index);
        if (currRange.isShorterThan(bestRange)) {
            bestRange.setRange(currRange);
        }
    }
    return bestRange;
}
```

### Time Complexity

- let S be length of shorter array
- let B be length of longer array


- `makeLists()` takes `O(S + B)`
- `getSmallestRange()` takes `O(B log S)` time.
-  Summing these 2 values, we get total time complexity becomes `O(S + B log S)`


### Space Complexity

`O(S)` for storage of our `PriorityQueue`

#### Question

Imagine you are reading in a stream of integers. Periodically, you wish to be able to look up the rank of a number x (the number of values less than or equal to x). Implement the data structures and algorithms to support these operations. That is, implement the method `track(int x)`, which is called when each number is generated, and the method `getRankOfNumber(int x)`, which returns the number of values less than or equal to X (not including x itself).

#### Example

- Stream (in order of appearance): 5, 1, 4, 4, 5, 9, 7, 13, 3
- getRankOfNumber(l) = 0
- getRankOfNumber(3) = 1
- getRankOfNumber(4) = 3

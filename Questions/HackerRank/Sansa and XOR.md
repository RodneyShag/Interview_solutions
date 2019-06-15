### Question

Given an array of integers:
1. XOR the values in every contiguous subarray together, then
1. XOR the above results together

Example:

```
Subarray  Operation	  Result
3         None           3
4         None           4
5         None           5
3,4       3 XOR 4        7
4,5       4 XOR 5        1
3,4,5     3 XOR 4 XOR 5  2
```

Then XOR the results: 3 ⊕ 4 ⊕ 5 ⊕ 7 ⊕ 1 ⊕ 2 = 6
### HackerRank Full Question

[Sum vs XOR](https://www.hackerrank.com/challenges/sum-vs-xor)

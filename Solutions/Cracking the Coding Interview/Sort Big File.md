### Solution

Use an [External Sort](https://en.wikipedia.org/wiki/External_sorting) such as External Merge Sort

1. We will assume that 20 gigabytes of data is too big to bring into memory.
1. Let's assume we have "x" megabytes of memory (where x < 20 gigabytes)
1. Divide the 20 gigabyte file into chunks of "x" megabytes each.
1. Sort each chunk separately (this can be done in parallel) and save it back to the file system.
1. Merge the chunks together into a fully sorted file.

### Time

__O(n log n)__ just like standard Merge Sort

### Space Complexity

- __O(n)__ space is needed for storage of this data on a hard disk.
- However, since we only have "x" megabytes of memory, our space complexity is __O(x)__
- If we could fully parallelize our algorithm onto enough machines of "x" bytes each and be sorting the entire 20 gigabytes in chunks simultaneously, then total space complexity is __O(n)__ (distributed onto multiple machines)

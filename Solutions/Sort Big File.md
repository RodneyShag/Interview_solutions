#### Solution

- External Sort
  1. We will assume that 20 gigabytes of data is too big to bring into memory.
  1. Let's assume we have "x" megabytes of memory (where x < 20 gigabytes)
  1. We'll divide the 20 gigabyte file into chunks of "x" megabytes each.
  1. Next, we sort each chunk separately and save it back to the file system.
  1. Finally, merge the chunks together into a fully sorted file.

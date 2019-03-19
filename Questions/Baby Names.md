### Question

Each year, the government releases a list of the 10000 most common baby names and their frequencies (the number of babies with that name). The only problem with this is that some names have multiple spellings. For example, "John" and "Jon" are essentially the same name but would be listed separately in the list. Given two lists, one of names/frequencies and the other of pairs of equivalent names, write an algorithm to print a new list of the true frequency of each name. Note that if John and Jon are synonyms, and Jon and Johnny are synonyms, then John and Johnny are synonyms. (It is both transitive and symmetric.) In the final list, any name can be used as the "real" name.

### Example

- Input:
  - Names: John (15), Jon (12), Chris (13), Kris (4), Christopher (19)
  - Synonyms: (Jon, John), (John, Johnny), (Chris, Kris), (Chris, Christopher)
- Output: John (27), Kris (36)

### Question

You are given 2 fields as input:
1. A string representing a corrupted test document in which all punctuation has vanished. For example: "itwasthebestoftimes".
1. A dictionary in the form of a boolean function `dict` such that, for any string `w`:

```
dict(w) =

true   if w is a valid word
false  otherwise
```

Using the above 2 inputs, determine if the test document is valid, in that it is just a concatenation of dictionary words.

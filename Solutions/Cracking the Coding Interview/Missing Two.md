# Solution - Finding 1 missing number

- Calculate the actual sum of 1 to n is (n)(n+1)/2
- Sum up the `n-1` values in the array.
- The difference of these 2 numbers is our missing number.

### Time/Space Complexity

-  Time Complexity: O(n) to sum up the numbers in the array
- Space Complexity: O(n)

# Solution - Finding 2 missing numbers

Let's label the 2 missing numbers as `a` and `b`.

- Formula 1: Sum of 1 to n is (n)(n+1)/2
- Formula 2: Sum of squares of 1 to n is 1<sup>2</sup> + 2<sup>2</sup> + .... n<sup>2</sup>

The 2 formulas above give us:

- ActualSum + a + b = (n)(n+1)/2
- ActualSumOfSquares + a<sup>2</sup> + b<sup>2</sup> = 1<sup>2</sup> + 2<sup>2</sup> + .... n<sup>2</sup>


Since `n` is known, and `ActualSum` and `ActualSumOfSquares` can be calculated, this gives us 2 formulas with 2 unknowns: `a`, `b`. We can solve these 2 equations for `a` and `b` (giving us the 2 missing numbers)

Note: Instead of Formula #2, you may have tried to use `1*2*...*n` as a formula. We don't use that formula since it will likely cause integer overflow

### Time/Space Complexity

-  Time Complexity: `O(n)` to loop through array and calculate `ActualSum` and `ActualSumOfSquares`. Solving the formula with 2 equations and 2 unknowns is O(1) time.
- Space Complexity: `O(1)`

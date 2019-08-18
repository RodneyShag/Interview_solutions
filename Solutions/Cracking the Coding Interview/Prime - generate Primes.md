This algorithm is called [The Sieve of Eratosthenes](https://en.wikipedia.org/wiki/Sieve_of_Eratosthenes)

### Solution

```java
boolean[] generatePrimes(int max) {
    boolean[] flags = new boolean[max + 1];
    initialize(flags);
    int prime = 2;
    int sqrt = (int) Math.sqrt(max);
    while (prime <= sqrt) { // see comment in crossOff() to see why we stop at sqrt(max)
        crossOff(flags, prime);
        prime = getNextPrime(flags, prime);
    }
    return flags;
}

private void initialize(boolean[] flags) {
    flags[0] = false;
    flags[1] = false;
    for (int i = 2; i < flags.length; i++) {
        flags[i] = true;
    }
}

// Cross off multiples of prime from our array
private void crossOff(boolean[] flags, int prime) {
    // We can start with (prime*prime), because if we have k * prime, where k < prime,
    // this value would have already been crossed off in a prior call to this function
    for (int i = prime * prime; i < flags.length; i += prime) {
        flags[i] = false;
    }
}

public int getNextPrime(boolean[] flags, int prime) {
    for (int i = prime + 1; i < flags.length; i++) {
        if (flags[i] == true) {
            return i;
        }
    }
    return -1; // our boolean[] wasn't big enough so we couldn't find the next prime.
}
```

### Time Complexity

`crossOff()` is O(n). We have to run crossOff() for O(n) numbers, so we can say the time complexity is __O(n<sup>2</sup>)__.

However, this analysis did not take into account the `i += prime` step in `crossOff()`, nor `getNextPrime()` that skips over certain numbers. The actual time complexity is __O(n * log(log(n)))__ according to [this link](https://en.wikipedia.org/wiki/Sieve_of_Eratosthenes#Algorithmic_complexity), but understanding/explaining it during an interview is definitely not expected.


### Space Complexity

O(n) due to `boolean[] flags`

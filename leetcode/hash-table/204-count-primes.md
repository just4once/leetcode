### Question {#question}

Count the number of prime numbers less than a non-negative number, **n**.

**Example:**

```

```

### Thought Process {#thought-process}

1. Typical Sqrt Root \(TLE\)
   1. One way we can test a number, n,  is prime or not is simply try all the number between 2 and n - 1
   2. A little bit optimized way is test all the number up to sqrt root of n
   3. Time complexity for isPrime function, O\(n^0.5\) for all number up to n, is O\(n^1.5\)
   4. Space complexity O\(1\)
2. Sieve of Eratosthenes
   1. Every time we pick a number, we mark all its multiple as not prime. We can also use composite boolean array to save the initialization cost
   2. Time complexity O\(n\)
   3. Space complexity O\(n\)

### Solution

```java
class Solution {
    public int countPrimes(int n) {
        if (n <= 2) return 0;
        int count = 0;
        for (int i = 2; i < n; i++) {
            if (isPrime(i)) count++;
        }
        return count;
    }
    
    private boolean isPrime(int num) {
        for (int f = 2; f * f <= num; f++) {
            if (num % f == 0) return false;
        }
        return true;
    }
}
```

```java
class Solution {
    public int countPrimes(int n) {
        if (n <= 2) return 0;
        boolean[] prime = new boolean[n];
        Arrays.fill(prime, true);
        prime[0] = false;
        prime[1] = false;
        int count = 0;
        for (int i = 2; i < n; i++) {
            if (!prime[i]) continue;
            count++;
            for (int m = 2; m * i < n; m++) {
                prime[m * i] = false;
            }
        }
        return count;
    }
}
```

```java
class Solution {
    public int countPrimes(int n) {
        if (n <= 2) return 0;
        boolean[] composite = new boolean[n];
        int count = 0;
        for (int i = 2; i < n; i++) {
            if (composite[i]) continue;
            count++;
            for (int m = 2; m * i < n; m++) {
                composite[m * i] = true;
            }
        }
        return count;
    }
}
```

### Additional {#additional}




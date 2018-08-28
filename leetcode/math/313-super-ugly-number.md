# 313-super-ugly-number

## Question {#question}

[https://leetcode.com/problems/super-ugly-number/description/](https://leetcode.com/problems/super-ugly-number/description/)

Write a program to find the nth super ugly number.

Super ugly numbers are positive numbers whose all prime factors are in the given prime list primes of size k.

**Example:**

```text
[1, 2, 4, 7, 8, 13, 14, 16, 19, 26, 28, 32] is the sequence of the first 12 super ugly numbers
Given primes = [2, 7, 13, 19] of size 4.
```

1. 1 is a super ugly number for any given primes.
2. The given numbers in primes are in ascending order.
3. 0 &lt; k ≤ 100, 0 &lt; n ≤ 106, 0 &lt; primes\[i\] &lt; 1000.
4. The nth super ugly number is guaranteed to fit in a 32-bit signed integer.

## Thought Process {#thought-process}

1. Array
   1. Similar to [264-Ugly Number II](264-ugly-number-ii.md), we just have to loop through all the prime and update its id accordingly
   2. Time complexity O\(np\)
   3. Space complexity O\(n + p\)

## Solution

```java
class Solution {
    public int nthSuperUglyNumber(int n, int[] primes) {
        int[] ugly = new int[n];
        int[] pid = new int[primes.length];
    ugly[0] = 1;
    int nextUgly, id;
    for (int i = 1; i < n; i++) {
        nextUgly = Integer.MAX_VALUE;
                id = 0;
        for (int p = 0; p < pid.length; p++) {
            int possible = ugly[pid[p]] * primes[p];
            if (possible < nextUgly) {
                nextUgly = possible;
                id = p;
            } else if (possible == nextUgly) {
                pid[p]++;
            }
        }
        ugly[i] = nextUgly;
        pid[id]++;
    }
    return ugly[n - 1];
    }
}
```

## Additional {#additional}


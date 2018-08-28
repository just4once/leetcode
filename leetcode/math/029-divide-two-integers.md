# 029-divide-two-integers

## Question {#question}

[https://leetcode.com/problems/divide-two-integers/description/](https://leetcode.com/problems/divide-two-integers/description/)

Divide two integers without using multiplication, division and mod operator.

If it is overflow, return MAX\_INT.

**Example:**

```text

```

## Thought Process {#thought-process}

1. Convert to Long
   1. Use two variables to check the accumulative sum and multiplier
   2. While the dividend is still greater than divisor, we can increase out count
   3. We can speed up the count by multiplying by 2 using right shift
   4. Time complexity O\(log n\)
   5. Space complexity O\(1\)

## Solution

```java
class Solution {
    public int divide(int dividend, int divisor) {
        if (divisor == 1) return dividend;
    if (divisor == -1) {
        return dividend == Integer.MIN_VALUE ? Integer.MAX_VALUE : -dividend;
    }
    int ret = 0;
    boolean isNegative = (dividend < 0) ^ (divisor < 0) ? true : false;
    long ldividend = Math.abs((long) dividend);
    long ldivisor = Math.abs((long) divisor);
    while (ldividend >= ldivisor) {
        long multiple = 1, accum = ldivisor;
        while (ldividend >= (accum << 1)) {
            accum <<= 1;
            multiple <<= 1;
        }
        ret += multiple;
        ldividend -= accum;
    }
    return isNegative ? -ret : ret;
    }
}
```

## Additional {#additional}


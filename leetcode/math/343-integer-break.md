# 343-integer-break

## Question {#question}

[https://leetcode.com/problems/integer-break/description/](https://leetcode.com/problems/integer-break/description/)

Given a positive integer n, break it into the sum of at least two positive integers and maximize the product of those integers. Return the maximum product you can get.

For example, given n = 2, return 1 \(2 = 1 + 1\); given n = 10, return 36 \(10 = 3 + 3 + 4\).

 **Note:** You may assume that n is not less than 2 and not larger than 58.

**Example:**

```text

```

## Thought Process {#thought-process}

1. Observe Pattern
   1. n = 1 2 3 4 5 6 7   8   9   10
   2. s = 0 1 2 4 6 9 12 18 27 36
   3. Starting from 7, the number repeat as multiple of 3 of num\[i - 3\]
   4. Time complexity O\(n\)
   5. Space complexity O\(1\)
2. Math
   1. We can use the built-in pow function to return result directly
   2. Time complexity O\(1\)???
   3. Space complexity O\(1\)

## Solution

```java
class Solution {
    public int integerBreak(int n) {
        if (n < 4) return n - 1;
        int res = 1;
        while (n > 4) {
            res *= 3;
            n -= 3;
        }
        res *= n;
        return res;
    }
}
```

```java
class Solution {
    public int integerBreak(int n) {
        if (n < 4) return n - 1;
        int cof = 1, p = (n + 1) / 3 - 1;
        if (n % 3 == 1) cof = 4;
        else if (n % 3 == 2) cof = 2;
        else cof = 3;
        return cof * (int) Math.pow(3, p);
    }
}
```

## Additional {#additional}


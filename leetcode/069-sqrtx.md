### Question {#question}

[https://leetcode.com/problems/sqrtx/description/](https://leetcode.com/problems/sqrtx/description/)

Implement int sqrt\(int x\).

Compute and return the square root of x.

x is guaranteed to be a non-negative integer.

**Example:**

```
Input: 4
Output: 2
```

```
Input: 8
Output: 2
Explanation: The square root of 8 is 2.82842..., and since we want to return an integer, the decimal part will be truncated.
```

### Thought Process {#thought-process}

1. Binary Search
   1. Use lo and hi to track the possible range of root
   2. We return right 
   3. Time complexity O\(log x\)
   4. Space 
2. Newton's method
   1. We can guess a root and gradually refine the root until the new guessis very close to the previous guess
   2. r1 = r - f\(r\) /f'\(r\)
   3. f\(r\) = r^2 - x
   4. f'\(r\) = 2r
   5. r1 = r - \(r^2 - x\) / 2r = \(r - x/r\) /2
   6. Time complexity ??
   7. Space complexity ???

### Solution

```java
class Solution {
    public int mySqrt(int x) {
        if (x == 0) return 0;
        int lo = 1, hi = x;
        while (lo <= hi) {
            int mi = lo + (hi - lo) / 2;
            if (mi == x / mi) return mi;
            else if (mi < x / mi) lo = mi + 1;
            else hi = mi - 1;
        }
        return hi;
    }
}
```

```java
class Solution {
    public int mySqrt(int x) {
        long r = x;
        while (r * r > x) {
            r = (r + x / r) / 2;
        }
        return (int) r;
    }
}
```

### Additional




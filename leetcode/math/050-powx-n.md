### Question {#question}

[https://leetcode.com/problems/powx-n/description/](https://leetcode.com/problems/powx-n/description/)

Implement pow\(x, n\).

**Example:**

```
Input: 2.00000, 10
Output: 1024.00000
```

```
Input: 2.10000, 3
Output: 9.26100
```

### Thought Process {#thought-process}

1. Recurision
   1. We can multiply the x by itself and reduce the power by 2
   2. If the power is odd we need to multiply by the result of x \* x and n / 2 power by x
   3. Time complexity O\(log n\)
   4. Space complexity O\(log n\) due to recursion stack
2. Iterative

### Solution

```java
class Solution {
    public double myPow(double x, int n) {
        if (n == 0) return 1;
        if (n == Integer.MIN_VALUE) {
            x *= x;
            n /= 2;
        }
        if (n < 0) {
            x = 1/ x;
            n = -n;
        }
        return n % 2 == 0 ? myPow(x * x, n / 2) : x * myPow(x * x, n / 2);
    }
}
```

```java
class Solution {
    public double myPow(double x, int n) {
        if (x == 0) return 0;
        if (n == 0) return 1;
        if (n == Integer.MIN_VALUE) {
            x *= x;
            n /= 2;
        }
        if (n < 0) {
            x = 1/ x;
            n = -n;
        }
        double res = 1;
        while (n > 0) {
            if ((n & 1) == 1) res *= x;
            x *= x;
            n /= 2;
        }
        return res;
    }
}
```

### Additional {#additional}




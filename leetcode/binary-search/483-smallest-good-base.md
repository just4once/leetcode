### Question {#question}

[https://leetcode.com/problems/smallest-good-base/description/](https://leetcode.com/problems/smallest-good-base/description/)

For an integer n, we call k&gt;=2 a good base of n, if all digits of n base k are 1.

Now given a string representing n, you should return the smallest good base of n in string format.

**Example 1:**

```
Input: "13"
Output: "3"
Explanation: 13 base 3 is 111.
```

**Example 2:**

```
Input: "4681"
Output: "8"
Explanation: 4681 base 8 is 11111.
```

**Example 3:**

```
Input: "1000000000000000000"
Output: "999999999999999999"
Explanation: 1000000000000000000 base 999999999999999999 is 11.
```

**Note:**

1. The range of n is \[3, 10^18\].
2. The string representing n is always valid and will not have leading zeros.

### Thought Process {#thought-process}

1. Binary Search
   1. Define base to be k, and number of digits to be m
   2. n = 1 + k^1 + k^2 + ... + k^\(m-1\)
   3. Using geometric sequence summation, we know n = \(1 - k^m\)/\(1 - k\)
   4. To find the bound for m and k, we need to use the above formula and other observation
   5. There is one trivial solution when k = n - 1, then m = 2
   6. When k = 2, which leads to n = 2^m - 1, then m = log\(n + 1\)
   7. Since we at looking for the minimum k, we start with maximum m
   8. Time complexity O\(mlogn\)
   9. Space complexity O\(1\)

### Solution

```java
import java.math.*;

class Solution {
    public String smallestGoodBase(String n) {
        long nL = Long.valueOf(n);
        int mHi = (int) (Math.log(nL + 1) / Math.log(2));
        long res = nL - 1;
        for (int m = mHi; m >= 2; m--) {
            System.out.println("current m = " + m);
            long kLo = 2, kHi = nL - 1;
            while (kLo <= kHi) {
                long kMi = kLo + (kHi - kLo) / 2;
                BigInteger left = BigInteger.valueOf(nL).multiply(BigInteger.valueOf(kMi - 1)), right = BigInteger.valueOf(kMi).pow(m).subtract(BigInteger.valueOf(1));
                int cmp = left.compareTo(right);
                if (cmp == 0) return String.valueOf(kMi);
                else if (cmp < 0) kHi = kMi - 1;
                else kLo = kMi + 1;
            }
        }
        return String.valueOf(res);
    }
}
```

### Additional {#additional}




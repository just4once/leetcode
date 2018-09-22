# 793-preimage-size-of-factorial-zeroes-function

## Question {#question}

[https://leetcode.com/problems/preimage-size-of-factorial-zeroes-function/description/](https://leetcode.com/problems/preimage-size-of-factorial-zeroes-function/description/)

Let f\(x\) be the number of zeroes at the end of x!. \(Recall that x! = 1  _2_  3  _..._  x, and by convention, 0! = 1.\)

For example, f\(3\) = 0 because 3! = 6 has no zeroes at the end, while f\(11\) = 2 because 11! = 39916800 has 2 zeroes at the end. Given K, find how many non-negative integers x have the property that f\(x\) = K.

**Example:**

```text
Example 1:
Input: K = 0
Output: 5
Explanation: 0!, 1!, 2!, 3!, and 4! end with K = 0 zeroes.

Example 2:
Input: K = 5
Output: 0
Explanation: There is no x such that x! ends in K = 5 zeroes.
```

**Note:**

K will be an integer in the range \[0, 10^9\].

## Thought Process {#thought-process}

1. Binary Search
   1. The number of trailing zeroes increase every time we have multiplication result of 10, meaning factor of 5 and 2
   2. So, the number of zeroes = min\(num of 2's, num of 5's\), and because of factor 2 appear at least every other number, we can simply count the number of factor 5
   3. For each x, K &lt;= x &lt; 5K + 1
   4. Performing binary search on this borders until the borders meet
   5. If we have found a value where we have exactly K zeroes, we can return 5
   6. Else there is no possible way to have K zeroes we return 0
   7. Time complexity O\(logK\)
   8. Space complexity O\(1\)

## Solution

```java
class Solution {
    public int preimageSizeFZF(int K) {
        // x / 5 <= f(x) <= x
        // so x >= K && x <= 5K
        // Therefore x will in the range of [K, ]
        long lo = K, hi = 5L * K + 1;
        while (lo < hi) {
            long mi = lo + (hi - lo) / 2;
            int k = f(mi);
            if (k == K) return 5;
            else if (k < K) lo = mi + 1;
            else hi = mi - 1;
        }
        return 0;
    }
    
    private int f(long x) {
        int count = 0;
        while (x > 0) {
            x /= 5;
            count += x;
        }
        return count;
    }
}
```

## Additional {#additional}


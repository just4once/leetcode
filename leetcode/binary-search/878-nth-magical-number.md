# 878-nth-magical-number

## Question {#question}

[https://leetcode.com/problems/nth-magical-number/description/](https://leetcode.com/problems/nth-magical-number/description/)

A positive integer is _magical_ if it is divisible by either A or B.

Return the N-th magical number.  Since the answer may be very large, **return it modulo** `10^9 + 7`.

1. 
**Example 1:**

```text
Input: N = 1, A = 2, B = 3
Output: 2
```

**Example 2:**

```text
Input: N = 4, A = 2, B = 3
Output: 6
```

**Example 3:**

```text
Input: N = 5, A = 2, B = 4
Output: 10
```

**Example 4:**

```text
Input: N = 3, A = 6, B = 4
Output: 8
```

**Note:**

1. `1 <= N <= 10^9`
2. `2 <= A <= 40000`
3. `2 <= B <= 40000`

## Thought Process {#thought-process}

1. Binary Search
   1. The magical number is always bounded between min\(A, B\) and min\(A, B\) \* N, lo and hi respectively
   2. Let's define A to be the smaller of two
   3. For every magical number, we count those numbers smaller than it and compare with N
   4. If we don't have enough count, we need to set lo = mi + 1
   5. Else hi = mi
   6. The count can be found by mi / A + mi / B - mi / L, where L is least common multiplier
   7. Time complexity O\(log\(N \* min\(A, B\)\)
   8. Space complexity O\(1\)
2. Math
   1. If we make close observation on the number, we can see that the numbers appear in chunk
   2. For example, if A = 2, B = 3, \[2, 3, 4, 6\] -&gt; \[8, 9, 10, 12\] -&gt; \[14, 15, 16, 18\], where addition of LCM\(A, B\) to each of the element will be the next chunk
   3. So, if we can get the first sequence under the LCM\(A, B\), we can get the Nth number \(N - 1\) / L \* LCM + chunk\[\(N - 1\) % L\], where L = length of chunk and L = LCM / A + LCM / B - 1
   4. Time complexity O\(A +B\)
   5. Space complexity O\(1\)

## Solution

```java
class Solution {
    public int nthMagicalNumber(int N, int A, int B) {
        if (A > B) return nthMagicalNumber(N, B, A);
        int M = (int) 1e9 + 7;
        if (B % A == 0) return (int) ((1L * A * N) % M);
        long L = A / gcd(A, B) * B;
        long lo = A, hi = lo * N;
        while (lo < hi) {
            long mi = lo + (hi - lo) / 2;
            long c = mi / A + mi / B - mi / L;
            if (c < N) lo = mi + 1;
            else hi = mi;
        }
        return (int) (lo % M);
    }
    
    private int gcd (int a, int b) {
        if (b == 0) return a;
        return gcd(b, a % b);
    }
}
```

```java
class Solution {
    public int nthMagicalNumber(int N, int A, int B) {
        int MOD = 1_000_000_007;
        int gcd = gcd(A, B), lcm = A * B / gcd;
        int L = lcm / A + lcm / B  - 1;
        int c = (N - 1) / L , d = (N - 1) % L;
        long ans = (long) c * lcm;
        int[] nums = {A, B};
        for (int i = 0; i < d; i++) {
            if (nums[0] <= nums[1]) nums[0] += A;
            else nums[1] += B;
        }
        ans += Math.min(nums[0], nums[1]);
        return (int) (ans % MOD);
    }
    
    private int gcd (int a, int b) {
        if (b == 0) return a;
        return gcd(b, a % b);
    }
}
```

## Additional {#additional}


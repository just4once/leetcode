### Question {#question}

[https://leetcode.com/problems/maximum-length-of-repeated-subarray/description/](https://leetcode.com/problems/maximum-length-of-repeated-subarray/description/)

Given two integer arrays A and B, return the maximum length of an subarray that appears in both arrays.

**Example:**

```
Input:
A: [1,2,3,2,1]
B: [3,2,1,4,7]
Output: 3
Explanation: 
The repeated subarray with maximum length is [3, 2, 1].
```

**Note:                  
**

1. 1 &lt;= len\(A\), len\(B\) &lt;= 1000
2. 0 &lt;= A\[i\], B\[i\] &lt; 100

### Thought Process {#thought-process}

1. Brute Force \(TLE\)
   1. Loop through all the elements in A and B, and check the corresponding matchness
   2. If the elements match, we check as far as we can and then get the maximum length
   3. Else we skip
   4. Time complexity O\(mn^2\)
   5. Space complexity O\(1\)
2. Naive Binary Search
   1. Having length k subarray appear in both array indicates having shorter length of subarray as well
   2. Using the above fact, we can use binary search to narrow our search
   3. We create a separate function checkLength\(x, A, B\) to check if there is length x subarray common to both arrays
   4. If x is checked, we need to continue search the right part, so lo = mi
   5. Else hi = mi
   6. However, we need special formula to take care of infinite loop to make mi calculation right leaning
   7. Time complexity O\(mnl\(logl\)\), where m is length of A, n is length of B, l is min of m and n
   8. Space complexity O\(m^2\)
3. Dynamic Programing
   1. Use similar idea as typical longest subsequence of string, we use dynamic programing to record the best length so far
   2. If the integers are the same for ith A and jth B element, we set dp\[i\]\[j\] = dp\[i - 1\]\[j - 1\] + 1
   3. Else we set dp\[i\]\[j\] = Math.max\(dp\[i - 1\]\[j\], dp\[i\]\[j - 1\], dp\[i - 1\]\[j - 1\]\)
   4. Time complexity O\(mn\)
   5. Space complexity O\(mn\)
4. Binary Search with Rolling Hash
   1. Instead of using string to check whether the two subarrays are equal, we use hash
   2. To efficiently calculate the hash, we use rolling hash function, more specifically Rabin-Karp algorithm
   3. The formula is h\(i\) = Sum\(a\[i\]p^i\) mod M, where i range from  0 to L - 1, calculating the next hash is h\(i+1\) = \[\(h\(i\) - a\[0\]\)/p + a\[i+1\]p^\(L - 1\)\] mod M
   4. Using a map to store the A's hash and its indices, then we can loop through the hash from B
   5. Instead of relying in the hash, we double check whether these two subarrays match even if they have same hash
   6. Time complexity O\(log\(l\)\(m + n\)\), where l = min\(m, n\)
   7. Space complexity O\(m + n\)

### Solution

Brute Force

```java
class Solution {
    public int findLength(int[] A, int[] B) {
        int res = 0;
        for (int i = 0; i < A.length; i++) {
            for (int j = 0; j < B.length; j++) {
                if (A[i] == B[j]) {
                    int k = 1;
                    while (i + k < A.length && j + k < B.length && A[i + k] == B[j + k]) k++;
                    res = Math.max(res, k);
                }
            }
        }
        return res;
    }
}
```

Naive Binary Search

```java
class Solution {
    public int findLength(int[] A, int[] B) {
        int lo = 0, hi = Math.min(A.length, B.length);
        while (lo < hi) {
            int mi = lo + (hi - lo + 1) / 2;
            if (checkLength(mi, A, B)) lo = mi;
            else hi = mi - 1;
        }
        return lo;
    }

    private boolean checkLength(int x, int[] A, int[] B) {
        if (x == 0) return true;
        else if (x > Math.min(A.length, B.length)) return false;
        else {
            Set<String> seen = new HashSet<>();
            for (int i = 0; i + x <= A.length; i++) {
                seen.add(Arrays.toString(Arrays.copyOfRange(A, i, i + x)));
            }
            for (int i = 0; i + x <= B.length; i++) {
                if (seen.contains(Arrays.toString(Arrays.copyOfRange(B, i, i + x)))) {
                    return true;
                }
            }
            return false;
        }
    }
}
```

DP

```java
class Solution {
    public int findLength(int[] A, int[] B) {
        int m = A.length, n = B.length;
        int[][] dp = new int[m + 1][n + 1];
        int ans = 0;
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                if (A[i] == B[j]) {
                    dp[i + 1][j + 1] = dp[i][j] + 1;
                    ans = Math.max(ans, dp[i + 1][j + 1]);
                }
            }
        }
        return ans;
    }
}
```

Binary Search with Rolling Hash

### Additional {#additional}




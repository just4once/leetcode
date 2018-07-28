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
   4. Our binary search needs to maintain the invariant that checkLength\(hi, A, B\) always return false, otherwise we will stuck in infinite loop
   5. Time complexity O\(mnl\(logl\)\), where m is length of A, n is length of B, l is min of m and n
   6. Space complexity O\(m^2\)
3. ads

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

```java
class Solution {
    public int findLength(int[] A, int[] B) {
        int lo = 0, hi = Math.min(A.length, B.length) + 1;
        while (lo < hi) {
            int mi = lo + (hi - lo) / 2;
            if (checkLength(mi, A, B)) lo = mi + 1;
            else hi = mi;
        }
        return lo - 1;
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

### Additional {#additional}




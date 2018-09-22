# 852-peak-index-in-a-mountain-array

## Question {#question}

[https://leetcode.com/problems/peak-index-in-a-mountain-array/description/](https://leetcode.com/problems/peak-index-in-a-mountain-array/description/)

Let's call an array A a mountain if the following properties hold:

A.length &gt;= 3 There exists some 0 &lt; i &lt; A.length - 1 such that A\[0\] &lt; A\[1\] &lt; ... A\[i-1\] &lt; A\[i\] &gt; A\[i+1\] &gt; ... &gt; A\[A.length - 1\] Given an array that is definitely a mountain, return any i such that A\[0\] &lt; A\[1\] &lt; ... A\[i-1\] &lt; A\[i\] &gt; A\[i+1\] &gt; ... &gt; A\[A.length - 1\].

**Example:**

```text
Input: [0,1,0]
Output: 1

Input: [0,2,1,0]
Output: 1
```

**Note:**

3 &lt;= A.length &lt;= 10000 0 &lt;= A\[i\] &lt;= 10^6 A is a mountain, as defined above.

## Thought Process {#thought-process}

1. Binary Search
   1. Since there is only one peak, we can use binary search to successively cut the search range by half
   2. The boundaries are lo = 1, hi = A.length - 2
   3. We compare A\[mi\] to A\[mi + 1\]
   4. If A\[mi\] &lt; A\[mi + 1\], the peak lies on the right, so lo = mi + 1
   5. Else hi = mi
   6. Time complexity O\(logn\)
   7. Space complexity O\(1\)

## Solution

```java
class Solution {
    public int peakIndexInMountainArray(int[] A) {
        int lo = 1, hi = A.length - 2;
        while (lo < hi) {
            int mi = lo + (hi - lo) / 2;
            if (A[mi] < A[mi + 1]) lo = mi + 1;
            else hi = mi;
        }
        return lo;
    }
}
```

## Additional {#additional}


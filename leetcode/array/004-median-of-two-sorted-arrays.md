### Question {#question}

[https://leetcode.com/problems/median-of-two-sorted-arrays/description/](https://leetcode.com/problems/median-of-two-sorted-arrays/description/)

There are two sorted arrays **nums1 **and **nums2 **of size m and n respectively.

Find the median of the two sorted arrays. The overall run time complexity should be O\(log \(m+n\)\).

**Example 1:**

```
nums1 = [1, 3]
nums2 = [2]

The median is 2.0
```

**Example 2:**

```
nums1 = [1, 2]
nums2 = [3, 4]

The median is (2 + 3)/2 = 2.5
```

### Thought Process {#thought-process}

1. Brute Force
   1. Knowing the length of both array, we can use a counter to count the element until it reach n/2 for odd number or n/2 + 1, and taking average for the second case
   2. Time complexity will be O\(m+ n\)
   3. Space complexity will be O\(1\)
2. Optimal \(Binary Search\)  
   1. Because the question warrants O\(log\(m+n\)\), binary search is probably the desired approach  
   2. Looking back at the definition of median of an array, it's located in the middle  
   3. If we can cut an array into two puts, and call the element immediately left to the cut L, and right to the cut the R, we can find the median easily by average them  
      1. \[2 3 / 5 7\] -&gt; median = \(3+5\)/2  
      2. \[2 3 \(4/4\) 5 7\] -&gt; median = \(4 + 4\) / 2 = 4

   1. The index can be listed as follow

      1. ```
         N        Index of L / R
         1               0 / 0
         2               0 / 1
         3               1 / 1  
         4               1 / 2      
         5               2 / 2
         6               2 / 3
         7               3 / 3
         8               3 / 4
         ```

         The formula is derived as \(L + R\)/2 = \(A\[\(N-1\)/2\] + A\[N/2\]\)/2

      2. For two arrays, we need to add some padding to make the index more consistent

   2. ```
      [6 9 13 18]  ->   [# 6 # 9 # 13 # 18 #]    (N = 4)
      position index     0 1 2 3 4 5  6 7  8     (N_Position = 9)

      [6 9 11 13 18]->   [# 6 # 9 # 11 # 13 # 18 #]   (N = 5)
      position index      0 1 2 3 4 5  6 7  8 9 10    (N_Position = 11)
      ```

      There are always 2N + 1 position and the cut is always at N position

   3. Observe that index\(L\) = \(N - 1\) / 2, and index\(R\) = N / 2

   4. There are 2N1 + 2N2 + 2 position altogether. Because we made two cuts on two arrays, there should be N1 + N2 on each side

   5. If we made the cut C2 = K in A2, then the C1 = N1 + N2 - K.

   6. Then we have two L's and two R's

      1. ```
          [# 1 # 2 # 3 # (4/4) # 5 #]    

          [# 1 / 1 # 1 # 1 #]
         ```
      2. ```
          L1 = A1[(C1-1)/2]; R1 = A1[C1/2];
          L2 = A2[(C2-1)/2]; R2 = A2[C2/2];
         ```
      3. ```
             L1 = A1[(7-1)/2] = A1[3] = 4; R1 = A1[7/2] = A1[3] = 4;
             L2 = A2[(2-1)/2] = A2[0] = 1; R2 = A1[2/2] = A1[1] = 1;
         ```
      4. We need to make sure L1 &lt;= R1 && L1 &lt;= R2 && L2 &lt;= R1 && L2 &lt;= R2

         1. Since arrays are sorted, we can drop L1 &lt;= R1 and L2 &lt;= R2 conditions, just focus on L1 &lt;= R2 and L2 &lt;= R1

         2. If L1 &gt; R2, we have too many large elements on left of A1, we need to move C1 to left or C2 to the right

         3. If L2 &gt; R1, we have too many large elements on left of A2, we need to move C2 to the left

      5. Because C1 and C2 are mutually determinable, we can just pick one. However, it's much more practical to use the shorter array as the basis, since all cut position on it is possible median. On the longer array, the position too far to the left or right is simply impossible.

   7. For instance, \[1\], \[2 3 4 5 6 7 8\].
      1. Corner cases are when C2 == 0 and C2 == 2N2, where we can insert a imaginary element A\[-1\] = INT\_MIN and A\[2N2\] = INT\_MAX

### Solution

Specifically address the odd length, return the min of right side, since right side has more elements.

```java
class Solution {
    public double findMedianSortedArrays(int[] nums1, int[] nums2) {
        int N1 = nums1.length, N2 = nums2.length;
        // We want to have smaller array as the second input
        if (N1 < N2) return findMedianSortedArrays(nums2, nums1);
        // The reason is that if we use pointers on the larger array,
        // the index of smaller array might be larger than its length.
        // The indice of smaller array are all potential cut.
        // @param halfLen store how many element we need to have on each side
        int lo = 0, hi = N2, halfLen = (N1 + N2) / 2;
        double L1 = Double.NaN, L2 = Double.NaN, R1 = Double.NaN, R2 = Double.NaN;
        while (lo <= hi) {
            // These two variables are the indice of R1 and R2
            // If the total length is odd, we will have an extra
            // element on the right.
            int mid2 = lo + (hi - lo) / 2;
            int mid1 = halfLen - mid2;
            L1 = mid1 == 0 ? Integer.MIN_VALUE : nums1[mid1 - 1];
            L2 = mid2 == 0 ? Integer.MIN_VALUE : nums2[mid2 - 1];
            R1 = mid1 == N1 ? Integer.MAX_VALUE : nums1[mid1];
            R2 = mid2 == N2 ? Integer.MAX_VALUE : nums2[mid2];
            if (L1 > R2) lo++;
            else if (L2 > R1) hi--;
            else {
                if ((N1 + N2) % 2 == 1) return Math.min(R1, R2);
                else break;
            }
        }
        return (Math.max(L1, L2) + Math.min(R1, R2)) / 2;
    }
}
```

With position padding, the code is slightly simpler.

```java
class Solution {
    public double findMedianSortedArrays(int[] nums1, int[] nums2) {
        int N1 = nums1.length, N2 = nums2.length;
        // We want to have smaller array as the second input
        if (N1 < N2) return findMedianSortedArrays(nums2, nums1);
        // The reason is that if we use pointers on the larger array,
        // the index of smaller array might be larger than its length.
        // The indice of smaller array are all potential cut
        int lo = 0, hi = 2 * N2;
        double L1 = Double.NaN, L2 = Double.NaN, R1 = Double.NaN, R2 = Double.NaN;
        while (lo <= hi) {
            int mid2 = lo + (hi - lo) / 2;
            int mid1 = N1 + N2 - mid2;
            L1 = mid1 == 0 ? Integer.MIN_VALUE : nums1[(mid1 - 1)/2];
            L2 = mid2 == 0 ? Integer.MIN_VALUE : nums2[(mid2 - 1)/2];
            R1 = mid1 == 2 * N1 ? Integer.MAX_VALUE : nums1[mid1/2];
            R2 = mid2 == 2 * N2 ? Integer.MAX_VALUE :nums2[mid2/2];
            if (L1 > R2) lo = mid2 + 1;
            else if (L2 > R1) hi = mid2 - 1;
            else break;
        }
        return (Math.max(L1, L2) + Math.min(R1, R2)) / 2;
    }
}
```

### Additional {#additional}




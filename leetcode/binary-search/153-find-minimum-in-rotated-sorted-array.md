# 153-find-minimum-in-rotated-sorted-array

## Question {#question}

[https://leetcode.com/problems/find-minimum-in-rotated-sorted-array/description/](https://leetcode.com/problems/find-minimum-in-rotated-sorted-array/description/)

Suppose an array sorted in ascending order is rotated at some pivot unknown to you beforehand.

\(i.e., \[0,1,2,4,5,6,7\] might become \[4,5,6,7,0,1,2\]\).

Find the minimum element.

You may assume no duplicate exists in the array.

**Example:**

```text
Input: [3,4,5,1,2],
Output: 1
```

## Thought Process {#thought-process}

1. Two Pointers
   1. We use two pointers to track the start and the end of the array
   2. To determine the min is on left on right, we need to check the nums\[mid\] against nums\[lo\] or nums\[hi\]
   3. If we check nums\[mid\] against nums\[lo\], and it's greater than nums\[lo\], the result is non-deterministic, because it could be on either side, i.e. \[2, 4, 6\] or \[4, 6, 2\]
   4. However, if we check nums\[mid\] against nums\[hi\] and it's smaller than nums\[hi\], the min can definitely on the left including the mid element
   5. Time complexity O\(log n\)
   6. Space complexity O\(1\)

## Solution

```java
class Solution {
    public int findMin(int[] nums) {
        int lo = 0, hi = nums.length - 1;
        while (lo < hi) {
            int mi = lo + (hi - lo) / 2;
            // we have already find the min on the right side
            // we narrow down to search the left
            if (nums[mi] < nums[hi]) hi = mi;
            else lo = mi + 1;
        }
        return nums[lo];
    }
}
```

## Additional {#additional}


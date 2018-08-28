# 154-find-minimum-in-rotated-sorted-array-ii

## Question {#question}

[https://leetcode.com/problems/find-minimum-in-rotated-sorted-array-ii/description/](https://leetcode.com/problems/find-minimum-in-rotated-sorted-array-ii/description/)

Suppose an array sorted in ascending order is rotated at some pivot unknown to you beforehand.

\(i.e., \[0,1,2,4,5,6,7\] might become \[4,5,6,7,0,1,2\]\).

Find the minimum element.

The array may contain duplicates.

**Example 1:**

```text
Input: [1,3,5],
Output: 1
```

**Example 2:**

```text
Input: [2,2,2,0,1],
Output: 0
```

**Note:**

* This is a follow up for "[Find Minimum in Rotated Sorted Array](https://leetcode.com/problems/find-minimum-in-rotated-sorted-array/description/)".
* Would allow duplicates affect the run-time complexity? How and why?

## Thought Process {#thought-process}

1. Two Pointers
   1. Similar to previous question, we need to find where to find our minium
   2. We compare mid element to the end element
      1. When nums\[mi\] &lt; nums\[hi\], it's on the left, so we set hi = mi
      2. When nums\[mi\] &gt; nums\[hi\], is's on the right because the pivot point has to be on the right
      3. Lastly, when nums\[mi\] == nums\[hi\], we decrease the hi and keep finding
   3. Time complexity O\(n\)
   4. Space complexity O\(1\)

## Solution

```java
class Solution {
    public int findMin(int[] nums) {
        int lo = 0, hi = nums.length - 1;
        while (lo < hi) {
            int mi = lo + (hi - lo) / 2;
            if (nums[mi] < nums[hi]) hi = mi;
            else if (nums[mi] > nums[hi]) lo = mi + 1;
            else hi--;
        }
        return nums[lo];
    }
}
```

## Additional {#additional}


# 033-search-in-rotated-sorted-array

## Question {#question}

[https://leetcode.com/problems/search-in-rotated-sorted-array/description/](https://leetcode.com/problems/search-in-rotated-sorted-array/description/)

Suppose an array sorted in ascending order is rotated at some pivot unknown to you beforehand.

\(i.e., 0 1 2 4 5 6 7 might become 4 5 6 7 0 1 2\).

You are given a target value to search. If found in the array return its index, otherwise return -1.

You may assume no duplicate exists in the array.

**Example:**

```text

```

## Thought Process {#thought-process}

1. Brute Force
   1. Compare value one by one
   2. Time complexity O\(n\)
   3. Space complexity O\(1\)
2. Pivot + Binary Search
   1. Locate the pivot point, this will divide the array into two sorted part
   2. If the target is smaller than the rightest element we search from pivot point to the last element
   3. Otherwise we search from 0th index to the pivot point
   4. Do binary search on the selected side
   5. Time complexity O\(log n\)
   6. Space complexity O\(1\)
3. Modified Binary Search
   1. We find the mid point, two major possible cases
      1. The mid point is our target, we return immediately
      2. The mid point is not our target
         1. The left part is sorted, we compare with the left's boundary and decide which part to search
         2. The right part is sorted, we compare with the right's boundary and decide which part to search

## Solution

Pivot + Binary Search

```java
class Solution {
    public int search(int[] nums, int target) {
        if (nums== null || nums.length == 0) return -1;
        int pivot = getPivot(nums);
        int lo = 0, hi = nums.length - 1;
        if (target <= nums[hi]) lo = pivot;
        else hi = pivot - 1;
        while (lo <= hi) {
            int mid = lo + (hi - lo) / 2;
            if (nums[mid] == target) return mid;
            else if (nums[mid] < target) lo = mid + 1;
            else hi = mid - 1;
        }
        return -1;
    }

    public int getPivot(int[] nums) {
        int lo = 0, hi = nums.length - 1;
        while (lo < hi) {
            int mid = lo + (hi - lo) / 2;
            if (nums[mid] < nums[hi]) hi = mid;
            else lo = mid + 1;
        }
        return lo;
    }
}
```

Modified Binary search

```java
class Solution {
    public int search(int[] nums, int target) {
        if (nums== null || nums.length == 0) return -1;
        int lo = 0, hi = nums.length - 1;
        while (lo <= hi) {
            int mid = lo + (hi - lo) / 2;
            if (nums[mid] == target) {
                return mid;
            } else if (nums[lo] <= nums[mid]) {
                if (target >= nums[lo] && target < nums[mid]) hi = mid -1;
                else lo = mid + 1;
            } else {
                if (target > nums[mid] && target <= nums[hi]) lo = mid + 1;
                else hi = mid - 1;
            }
        }
        return -1;
    }
}
```

## Additional {#additional}


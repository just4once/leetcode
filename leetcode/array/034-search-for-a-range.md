# 034-search-for-a-range

## Question {#question}

[https://leetcode.com/problems/search-for-a-range/description/](https://leetcode.com/problems/search-for-a-range/description/)

Given an array of integers sorted in ascending order, find the starting and ending position of a given target value.

Your algorithm's runtime complexity must be in the order ofO\(logn\).

If the target is not found in the array, return`[-1, -1]`.

**Example:**

```text
Given [5, 7, 7, 8, 8, 10] and target value 8,
return [3, 4].
```

## Thought Process {#thought-process}

1. A requirement for O\(log n\) hints the use of binary search
2. However because we want the range, we need to use modified binary search
   1. We can try to find the left boundary, there are three cases here
      1. When the mid is too small, the range starts on the right of mid, so lo = mid + 1
      2. When the mid is too big, the range starts on the left of mid, so hi = mid -1
      3. When the mid is equal, the range starts on the left or at mid, so hi = mid
      4. Therefore we can combine ii and iii together and set hi = mid
   2. On the other hand, for the right boundary, we can similar conditions, which boils down to
      1. lo = mid
      2. hi = mid - 1
   3. Those above steps will make sure we are moving the pointers outward and find the border

## Solution

```java
class Solution {
    public int[] searchRange(int[] nums, int target) {
        int[] result = { -1, -1 };
        if (nums == null) return result;
        result[0] = searchLeft(nums, target, 0, nums.length - 1);
        result[1] = searchRight(nums, target, result[0], nums.length - 1);
        return result;
    }

    public int searchLeft(int[] nums, int target, int lo, int hi) {
        if (lo > hi || lo < 0) return -1;
        while (lo < hi) {
            int mid = lo + (hi - lo) / 2;
            if (nums[mid] < target) lo = mid + 1;
            else hi = mid;
        }
        return nums[lo] == target ? lo : -1;
    }

    public int searchRight(int[] nums, int target, int lo, int hi) {
        if (lo > hi || lo < 0) return -1;
        if (lo == hi) return nums[lo] == target ? lo : -1;
        while (lo < hi) {
            int mid = lo + (hi - lo) / 2 + 1;
            if (nums[mid] > target) hi = mid - 1;
            else lo = mid;
        }
        return nums[lo] == target ? lo : -1;
    }
}
```

Instead of writing two similar function, we can do a small trick. When we search found the right boundary, instead of searching target, we can search target + 1. Then deduct 1 from the result to get the correct position of right boundary.

```java
class Solution {
    public int[] searchRange(int[] nums, int target) {
        int[] result = { -1, -1 };
        if (nums == null || nums.length == 0) return result;
        int left = search(nums, target, 0, nums.length);
        if (left >= nums.length || (left >= 0 && nums[left] != target)) return result;
        result[0] = left;
        result[1] = search(nums, target + 1, left, nums.length) - 1;
        return result;
    }

    public int search(int[] nums, int target, int lo, int hi) {
        while (lo < hi) {
            int mid = lo + (hi - lo) / 2;
            if (nums[mid] < target) lo = mid + 1;
            else hi = mid;
        }
        return lo;
    }
}
```

## Additional {#additional}


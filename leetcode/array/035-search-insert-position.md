# 035-search-insert-position

## Question {#question}

[https://leetcode.com/problems/search-insert-position/description/](https://leetcode.com/problems/search-insert-position/description/)

Given a sorted array and a target value, return the index if the target is found. If not, return the index where it would be if it were inserted in order.

You may assume no duplicates in the array.

**Example 1:**

```text
Input: [1,3,5,6], 5
Output: 2
```

**Example 2:**

```text
Input: [1,3,5,6], 2
Output: 1
```

## Thought Process {#thought-process}

1. Basically this is regular binary search

## Solution

```java
class Solution {
    public int searchInsert(int[] nums, int target) {
        if(nums == null) return -1;
        int lo = 0, hi = nums.length - 1;
        while (lo <= hi){
            int mid = lo + (hi - lo)/2;
            if (nums[mid] == target) return mid;
            else if (nums[mid] < target) lo = mid + 1;
            else hi = mid - 1;
        }
        return lo;
    }
}
```

## Additional {#additional}


# 704-binary-search

## Question {#question}

[https://leetcode.com/problems/binary-search/description/](https://leetcode.com/problems/binary-search/description/)

Given a sorted \(in ascending order\) integer array nums of n elements and a target value, write a function to search target in nums. If target exists, then return its index, otherwise return -1.

**Example 1:**

```text
Input: nums = [-1,0,3,5,9,12], target = 9
Output: 4
Explanation: 9 exists in nums and its index is 4
```

**Example 2:**

```text
Input: nums = [-1,0,3,5,9,12], target = 2
Output: -1
Explanation: 2 does not exist in nums so return -1
```

**Note:** 

1. You may assume that all elements in nums are unique.
2. n will be in the range \[1, 10000\].
3. The value of each element in nums will be in the range \[-9999, 9999\].

## Thought Process {#thought-process}

1. Binary
   1. Time complexity O\(logn\)
   2. Space complexity O\(1\)

## Solution

```java
class Solution {
    public int search(int[] nums, int target) {
        int lo = 0, hi = nums.length - 1;
        while (lo <= hi) {
            int mi = lo + (hi - lo) / 2;
            if (nums[mi] == target) return mi;
            else if (nums[mi] < target) lo = mi + 1;
            else hi = mi - 1;
        }
        return -1;
    }
}
```

## Additional {#additional}


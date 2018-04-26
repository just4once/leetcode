### Question {#question}

[https://leetcode.com/problems/find-peak-element/description/](https://leetcode.com/problems/find-peak-element/description/)

A peak element is an element that is greater than its neighbors.

Given an input array nums, where num\[i\] ≠ num\[i+1\], find a peak element and return its index.

The array may contain multiple peaks, in that case return the index to any one of the peaks is fine.

You may imagine that num\[-1\] = num\[n\] = -∞.

**Example 1:**

```
Input: nums = [1, 2, 3, 1]
Output: 2
Explanation: 3 is a peak element and your function should return the index number 2.
```

**Example 2:**

```
Input: nums = [1, 2, 1, 3, 5, 6, 4]
Output: 1 or 5 
Explanation: Your function can return either index number 1 where the peak element is 2, 
             or index number 5 where the peak element is 6.
```

### Thought Process {#thought-process}

1. One Pointer
   1. Starting from second element, or nums\[1\], if the current number is smaller than the previous number, the previous number has to be a peak
   2. If the element is all increasing then the last number has to be the peak
   3. Time complexity O\(n\)
   4. Space complexity O\(1\)
2. Recursion - Binary Search
   1. We search the array with binary search approach
   2. To determine the side we go to, we need to check current exploring element with its next element \(because the mid formula is left-leaning\)
   3. If the number is greater than 
   4. Time complexity O\(log n\)
   5. Space complexity O\(log n\) due to recursion
3. Iteration
   1. Time complexity O\(log n\)
   2. Space complexity O\(1\)

### Solution

```java
class Solution {
    public int findPeakElement(int[] nums) {
        for (int i = 1; i < nums.length; i++){
            if (nums[i] < nums[i-1]) return i -1;
        }
        return nums.length - 1;
    }
}
```

```java
class Solution {
    public int findPeakElement(int[] nums) {
        return find(nums, 0, nums.length - 1);
    }
    
    private int find(int[] nums, int i, int j) {
        if (i == j) return i;
        int m = i + (j - i) / 2;
        if (nums[m] > nums[m + 1]) return find(nums, i, m);
        else return find(nums, m + 1, j);
    }
}
```

```java
class Solution {
    public int findPeakElement(int[] nums) {
        int i = 0, j = nums.length - 1;
        while (i < j) {
            int m = i + (j - i) / 2;
            if (nums[m] > nums[m + 1]) j = m;
            else i = m + 1;
        }
        return i;
    }
}
```

### Additional {#additional}




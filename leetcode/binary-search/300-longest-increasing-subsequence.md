# 300-longest-increasing-subsequence

## Question {#question}

[https://leetcode.com/problems/longest-increasing-subsequence/description/](https://leetcode.com/problems/longest-increasing-subsequence/description/)

Given an unsorted array of integers, find the length of longest increasing subsequence.

For example,

Given **\[10, 9, 2, 5, 3, 7, 101, 18\]**,

The longest increasing subsequence is **\[2, 3, 7, 101\]**, therefore the length is **4**. Note that there may be more than one LIS combination, it is only necessary for you to return the length.

Your algorithm should run in O\(n2\) complexity.

Follow up: Could you improve it to O\(n log n\) time complexity?

**Example:**

```text

```

## Thought Process {#thought-process}

1. Dynamic Programing
   1. Using dp array to store the longest length ending, where dp\[i\] stores the information for sequence ending with ith element
   2. Time complexity O\(n^2\)
   3. Space complexity O\(n\)
2. Dynamic Programing with Binary Search
   1. Instead of storing the length for each element, we store the numbers
   2. For each number, we try to see if we can add this to to our existing sequence
   3. We use binary search to return the respective index, if the index is equal to the current length, we can add it and increase the length
   4. Otherwise we set the number at the correct index
   5. Time complexity O\(nlogn\)
   6. Space complexity O\(n\)

## Solution

```java
class Solution {
    public int lengthOfLIS(int[] nums) {
        if (nums == null || nums.length == 0) return 0;
        int n = nums.length;
        int[] dp = new int[n];
        dp[0] = 1;
        int maxLen = 0;
        for (int i = 1; i < n; i++) {
            int max = 0;
            for (int j = 0; j < i; j++) {
                if (nums[i] > nums[j]) max = Math.max(max, dp[j]);
            }
            dp[i] = max + 1;
            maxLen = Math.max(maxLen, dp[i]);
        }
        return maxLen;
    }
}
```

```java
class Solution {
    public int lengthOfLIS(int[] nums) {
        if (nums == null || nums.length == 0) return 0;
        int n = nums.length;
        int[] dp = new int[n];
        dp[0] = nums[0];
        int id = 0;
        for (int i = 1; i < n; i++) {
            if (nums[i] > dp[id]) {
                dp[++id] = nums[i];
            } else {
                int j = binarySearch(dp, 0, id, nums[i]);
                dp[j] = nums[i];
            }
        }
        return id + 1;
    }

    private int binarySearch(int[] nums, int start, int end, int target) {
        while (start <= end) {
            int mid = start + (end - start) / 2;
            if (nums[mid] == target) return mid;
            else if (nums[mid] < target) start = mid + 1;
            else end = mid - 1;
        }
        return start;
    }
}
```

## Additional {#additional}


# 410-split-array-largest-sum

## Question {#question}

[https://leetcode.com/problems/split-array-largest-sum/description/](https://leetcode.com/problems/split-array-largest-sum/description/)

Given an array which consists of non-negative integers and an integerm, you can split the array intomnon-empty continuous subarrays. Write an algorithm to minimize the largest sum among thesemsubarrays.

**Note:**  
Ifnis the length of array, assume the following constraints are satisfied:

* 1 ≤ n ≤ 1000
* 1 ≤ m ≤ min\(50, n\)

**Example:**

```text
Input:
nums = [7,2,5,10,8]
m = 2

Output:
18

Explanation:
There are four ways to split nums into two subarrays.
The best way is to split it into [7,2,5] and [10,8],
where the largest sum among the two subarrays is only 18.
```

## Thought Process {#thought-process}

1. Brute Force
   1. Cutting at every position, we have n - 1Cm - 1 possibilities
   2. Time complexity O\(n^m\)
   3. Space complexity O\(n\)
2. Dynamic Programing
   1. Create an array dp, and dp\[i\]\[j\] indicates the minimum of max sum splitting into i parts with j elements
   2. Since each new split depends on previous split and loop 1 parts to m parts using i pointer
   3. Also, current elements depends result of previous element range from 0 to j - 1
   4. Therefore, dp\[i\]\[j\] depends on dp\[i - 1\]\[k\] where k range from 0 to j - 1 \(or i - 1 to j - 1 because i - 1 is min index needed for having enough element for i parts\)
   5. Time complexity O\(n^2m\)
   6. Space complexity O\(n\)
3. Binary Search
   1. The result must lie between the max element and sum, referring as left and right pointer
   2. Using binary search to search the mid value, we count how many element we need to split
   3. If the count is greater than m, that mean our mid is too small so we need to increase our left pointer
   4. Otherwise we decrease the right pointer
   5. Time complexity O\(nlog\(s\)\) where n is number of elements and s is sum of array
   6. Space complexity O\(1\)

## Solution

```java
class Solution {
    private int res = Integer.MAX_VALUE;
    public int splitArray(int[] nums, int m) {
        dfs(nums, m, 0, 0, 0, 0);
        return res;
    }

    private void dfs(int[] nums, int m, int i, int j, int cur, int max) {
        if (i == nums.length && j == m) {
            res = Math.min(max, res);
            return;
        }
        if (i == nums.length) return;
        if (i > 0) dfs(nums, m, i + 1, j, cur + nums[i], Math.max(max, cur + nums[i]));
        if (j < m) dfs(nums, m, i + 1, j + 1, nums[i], Math.max(max, nums[i]));
    }
}
```

```java
class Solution {
    public int splitArray(int[] nums, int m) {
        int n = nums.length;
        int[] sum = new int[n + 1];
        int[][] dp = new int[2][n + 1];
        for (int i = 0; i < n; i++) {
            sum[i + 1] = nums[i] + sum[i];
            dp[0][i + 1] = Integer.MAX_VALUE;
            dp[1][i + 1] = Integer.MAX_VALUE;
        }
        for (int i = 1; i <= m; i++) {
            for (int j = 1; j <= n; j++) {
                for (int k = i - 1; k < j; k++) {
                    dp[i % 2][j] = Math.min(dp[i % 2][j], Math.max(dp[(i - 1) % 2][k], sum[j] - sum[k]));
                }
            }
        }
        return dp[m % 2][n];
    }
}
```

```java
class Solution {
    public int splitArray(int[] nums, int m) {
        int n = nums.length;
        long left = 0, right = 0;
        for (int num : nums) {
            left = Math.max(left, num);
            right += num;
        }
        if (m == 1) return (int) right;
        while (left < right) {
            long mid = left + (right - left) / 2;
            if (validGroup(nums, mid, m)) right = mid;
            else left = mid + 1;
        }
        return (int) right;
    }

    private boolean validGroup(int[] nums, long target, int m) {
        int count = 1;
        long sum = 0;
        for (int num : nums) {
            sum += num;
            if (sum > target) {
                count++;
                sum = num;
                if (count > m) return false;
            }
        }
        return true;
    }
}
```

## Additional {#additional}


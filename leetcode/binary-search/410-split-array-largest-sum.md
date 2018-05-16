### Question {#question}

[https://leetcode.com/problems/split-array-largest-sum/description/](https://leetcode.com/problems/split-array-largest-sum/description/)

Given an array which consists of non-negative integers and an integerm, you can split the array intomnon-empty continuous subarrays. Write an algorithm to minimize the largest sum among thesemsubarrays.

**Note:**  
Ifnis the length of array, assume the following constraints are satisfied:

* 1 ≤ n ≤ 1000
* 1 ≤ m ≤ min\(50, n\)

**Example:**

```
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

### Thought Process {#thought-process}

1. Brute Force
   1. Cutting at every position, we have n - 1Cm - 1 possibilities
   2. Time complexity O\(n^m\)
   3. Space complexity O\(n\)
2. Dynamic Programing
   1. Create an array dp, and dp\[i\]\[j\] indicates the minimum of max sum ending at ith element by splitting into j parts
   2. As we loop through each number using i pointer, we need to determine each of best min max splitting into j parts
   3. dp\[i\]\[j\] depends on dp\[k\]\[j - 1\], where k range from 0 to i - 1, and also on sum from k + 1th to ith numbers, where remaining numbers become a new part
3. asdsad

### Solution

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
        for (int i = 0; i < n; i++) {
            sum[i + 1] = nums[i] + sum[i];
        }
        int[][] dp = new int[n + 1][m + 1];
        for (int i = 0; i <= n; i++) {
            Arrays.fill(dp[i], Integer.MAX_VALUE);
        }
        dp[0][0] = 0;
        for (int i = 1; i <= n; i++) {
            for (int j = 1; j <= m; j++) {
                for (int k = 0; k < i; k++) {
                    dp[i][j] = Math.min(dp[i][j], Math.max(dp[k][j - 1], sum[i] - sum[k]));
                }
            }
        }
        return dp[n][m];
    }
}
```

### Additional {#additional}




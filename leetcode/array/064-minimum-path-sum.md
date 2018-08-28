# 064-minimum-path-sum

## Question {#question}

[https://leetcode.com/problems/minimum-path-sum/description/](https://leetcode.com/problems/minimum-path-sum/description/)

Given a m x n grid filled with non-negative numbers, find a path from top left to bottom right which minimizes the sum of all numbers along its path.

**Example:**

```text
[[1,3,1],
 [1,5,1],
 [4,2,1]]

Given the above grid map, return 7. Because the path 1→3→1→1→1 minimizes the sum.
```

## Thought Process {#thought-process}

1. Similar to the [062-Unique Paths](062-unique-paths.md) and [063-Unique Paths II ](063-unique-paths-ii.md)we can create two dimensional dp array and reduce to one dimentional

## Solution

```java
class Solution {
    public int minPathSum(int[][] grid) {
        if (grid == null || grid.length == 0) return 0;
        int m = grid.length, n = grid[0].length;
        int[] dp = new int[n + 1];
        for (int c = 1; c <= n; c++) dp[c] = dp[c - 1] + grid[0][c - 1];
        for (int r = 1; r < m; r++) {
            dp[0] = Integer.MAX_VALUE;
            for (int c = 1; c <= n; c++) {
                dp[c] = Math.min(dp[c], dp[c - 1]) + grid[r][c - 1];
            }
        }
        return dp[n];
    }
}
```

## Additional {#additional}


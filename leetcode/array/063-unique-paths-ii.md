### Question {#question}

[https://leetcode.com/problems/unique-paths-ii/description/](https://leetcode.com/problems/unique-paths-ii/description/)

Follow up for "Unique Paths":

Now consider if some obstacles are added to the grids. How many unique paths would there be?

An obstacle and empty space is marked as 1 and 0 respectively in the grid.

**Example:**

```
There is one obstacle in the middle of a 3x3 grid as illustrated below.
[
  [0,0,0],
  [0,1,0],
  [0,0,0]
]
```

### Thought Process {#thought-process}

1. Similar to [062-Unique Paths](/leetcode/array/062-unique-paths.md), we can create two dimensional array and reduce the space

### Solution

```java
class Solution {
    public int uniquePathsWithObstacles(int[][] obstacleGrid) {
        if (obstacleGrid == null || obstacleGrid.length == 0) return 0;
        int m = obstacleGrid.length, n = obstacleGrid[0].length;
        int[][] dp = new int[m][n];
        for (int c = 0; c < n && obstacleGrid[0][c] == 0; c++) dp[0][c] = 1;
        for (int r = 1; r < m && obstacleGrid[r][0] == 0 && dp[r - 1][0] != 0; r++) dp[r][0] = 1;
        for (int r = 1; r < m; r++) {
            for (int c = 1; c < n; c++) {
                if (obstacleGrid[r][c] == 0) {
                    dp[r][c] = dp[r - 1][c] + dp[r][c - 1];
                }
            }
        }
        return dp[m - 1][n - 1];
    }
}
```

```java
class Solution {
    public int uniquePathsWithObstacles(int[][] obstacleGrid) {
        if (obstacleGrid == null || obstacleGrid.length == 0) return 0;
        int m = obstacleGrid.length, n = obstacleGrid[0].length;
        int[] dp = new int[n];
        dp[0] = 1;
        for (int r = 0; r < m; r++) {
            for (int c = 0; c < n; c++) {
                if (obstacleGrid[r][c] == 0) {
                    dp[c] += c > 0 ? dp[c - 1] : 0;
                } else {
                    dp[c] = 0;
                }
            }
        }
        return dp[n - 1];
    }
}
```

### Additional {#additional}




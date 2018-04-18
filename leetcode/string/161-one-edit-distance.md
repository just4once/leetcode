### Question {#question}

Given two strings S and T, determine if they are both one edit distance apart.

**Example:**

```

```

### Thought Process {#thought-process}

1. DP \(TLE\)
   1. Typical DP where we store the edit distance in dp, where dp\[i\]\[j\] means the edit distance up to ith character of s and jth character of t
   2. Time complexity O\(mn\)
   3. Space complexity O\(mn\)
2. Two Pointers
   1. Using two pointers i and j to track the index of s and t respectively
   2. Another variable to check the difference we have encountered
   3. At the end, we just need to check whether the diff == 1 or diff == 0 && m != n
   4. Time complexity O\(m\)
   5. Space complexity O\(1\)

### Solution

```java
class Solution {
    public boolean isOneEditDistance(String s, String t) {
        int m = s.length(), n = t.length();
        int[][] dp = new int[m + 1][n + 1];
        char[] sc = s.toCharArray(), tc = t.toCharArray();
        for (int j = 1; j <= n; j++) dp[0][j] = j;
        for (int i = 1; i <= m; i++) dp[i][0] = i;
        for (int i = 1; i <= m; i++) {
            for (int j = 1; j <= n; j++) {
                if (sc[i - 1] == tc[j - 1]) dp[i][j] = dp[i - 1][j - 1];
                else dp[i][j] = Math.min(dp[i - 1][j - 1], Math.min(dp[i - 1][j], dp[i][j - 1])) + 1;
            }
        }
        return dp[m][n] == 1;
    }
}
```

### Additional {#additional}




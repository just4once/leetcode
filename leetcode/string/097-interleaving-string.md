# 097-interleaving-string

## Question {#question}

[https://leetcode.com/problems/interleaving-string/description/](https://leetcode.com/problems/interleaving-string/description/)

Given s1, s2, s3, find whether s3 is formed by the interleaving of s1 and s2.

**Example:**

```text
Given:
s1 = "aabcc",
s2 = "dbbca",

When s3 = "aadbbcbcac", return true.
When s3 = "aadbbbaccc", return false.
```

## Thought Process {#thought-process}

1. Recursion \(TLE\)
   1. From two strings, we can pick either one from s1 and s2
   2. For tracking usage of the characters from s1 and s2, we use two variables i and j
   3. As long we i and j is smaller than the length, we can add the character and recurse
   4. Time complexity O\(2^\(m + n\)\)
   5. Space complexity O\(2^\(m+n\)\) due to recursiong
2. Recursion with Memo
   1. Using three variables to track s1, s2 and s3
   2. When either i or j reach the end, we just need to check the rest of the other string
   3. Time complexity O\(m + n\)
   4. Space complexity O\(mn\) for memo and O\(m + n\) due to recursion
3. Dynamic Programing Bottom Up
   1. Create dp array of dimension m + 1 and n + 1, where m is length of s1 and n is length of s2
   2. dp\[i\]\[j\] indicates the possibility of using ith character of s1 or jth character of s2 for the kth character of s3, where k = i + j
   3. Time complexity O\(mn\)
   4. Space complexity O\(mn\)
4. DP with Space Reduction
   1. Time complexity O\(mn\)
   2. Space complexity O\(n\)

## Solution

```java
class Solution {
    public boolean isInterleave(String s1, String s2, String s3) {
        if (s1.length() + s2.length() != s3.length()) return false;
        return isInterleave(s1, 0, s2, 0, "", s3);
    }

    private boolean isInterleave(String s1, int i, String s2, int j, String res, String s3) {
        if (res.equals(s3)) return true;
        boolean ans = false;
        if (i < s1.length() && s3.charAt(i + j) == s1.charAt(i)) {
            ans |= isInterleave(s1, i + 1, s2, j, res + s1.charAt(i), s3);
        }
        if (j < s2.length() && s3.charAt(i + j) == s2.charAt(j)) {
            ans |= isInterleave(s1, i, s2, j + 1, res + s2.charAt(j), s3);
        }
        return ans;
    }
}
```

```java
class Solution {
    public boolean isInterleave(String s1, String s2, String s3) {
        if (s1.length() + s2.length() != s3.length()) return false;
        Boolean[][] memo = new Boolean[s1.length()][s2.length()];
        return isInterleave(s1, 0, s2, 0, s3, 0, memo);
    }

    private boolean isInterleave(String s1, int i, String s2, int j, String s3, int k, Boolean[][] memo) {
        if (i == s1.length()) return s2.substring(j).equals(s3.substring(k));
        if (j == s2.length()) return s1.substring(i).equals(s3.substring(k));
        if (memo[i][j] != null) return memo[i][j];
        boolean ans = false;
        if ((s1.charAt(i) == s3.charAt(k) && isInterleave(s1, i + 1, s2, j, s3, k + 1, memo)) || (s2.charAt(j) == s3.charAt(k) && isInterleave(s1, i, s2, j + 1, s3, k + 1, memo))) {
            ans = true;
        }
        memo[i][j] = ans;
        return ans;
    }
}
```

```java
class Solution {
    public boolean isInterleave(String s1, String s2, String s3) {
        if (s1.length() + s2.length() != s3.length()) return false;
        int m = s1.length(), n = s2.length();
        boolean[][] dp = new boolean[m + 1][n + 1];
        dp[0][0] = true;
        for (int j = 1; j <= n; j++) {
            if (dp[0][j - 1] && s2.charAt(j - 1) == s3.charAt(j - 1)) dp[0][j] = true;
        }
        for (int i = 1; i <= m; i++) {
            if (dp[i - 1][0] && s1.charAt(i - 1) == s3.charAt(i - 1)) dp[i][0] = true;
        }
        for (int i = 1; i <= m; i++) {
            for (int j = 1; j <= n; j++) {
                dp[i][j] = (dp[i][j - 1] && s2.charAt(j - 1) == s3.charAt(i + j - 1)) || (dp[i - 1][j] && s1.charAt(i - 1) == s3.charAt(i + j - 1));
            }
        }
        return dp[m][n];
    }
}
```

```java
class Solution {
    public boolean isInterleave(String s1, String s2, String s3) {
        if (s1.length() + s2.length() != s3.length()) return false;
        int m = s1.length(), n = s2.length();
        boolean[]dp = new boolean[n + 1];
        dp[0] = true;
        for (int j = 1; j <= n; j++) {
            if (dp[j - 1] && s2.charAt(j - 1) == s3.charAt(j - 1)) dp[j] = true;
        }
        for (int i = 1; i <= m; i++) {
            dp[0] = dp[0] && s1.charAt(i - 1) == s3.charAt(i - 1);
            for (int j = 1; j <= n; j++) {
                dp[j] = (dp[j - 1] && s2.charAt(j - 1) == s3.charAt(i + j - 1)) || (dp[j] && s1.charAt(i - 1) == s3.charAt(i + j - 1));
            }
        }
        return dp[n];
    }
}
```

## Additional {#additional}


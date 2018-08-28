# 115-distinct-subsequences

## Question {#question}

[https://leetcode.com/problems/distinct-subsequences/description/](https://leetcode.com/problems/distinct-subsequences/description/)

Given a string S and a string T, count the number of distinct subsequences of S which equals T.

A subsequence of a string is a new string which is formed from the original string by deleting some \(can be none\) of the characters without disturbing the relative positions of the remaining characters. \(ie, "ACE" is a subsequence of "ABCDE" while "AEC" is not\).

**Example:**

```text
Here is an example:
S = "rabbbit", T = "rabbit"

Return 3.
```

## Thought Process {#thought-process}

1. Dynamic programing
   1. Create an array of dp\[m + 1\]\[n + 1\], where m is the length of T and s is length of S
   2. dp\[i\]\[j\] stores the number of sequence for up to ith character of T and jth character of S
   3. The first row is filled with 1 because as an empty string is part of any strings
   4. The first column is filled with 0 because nonempty T will not be part of empty string
   5. If the current ith character doesn't match with jth character, we simply set dp\[i\]\[j\] = dp\[i\]\[j - 1\] which means we have same number as before without using new character
   6. If the current characters matches, we set dp\[i\]\[j\] = dp\[i\]\[j - 1\] + dp\[i - 1\]\[j -1\], which means whatever we have before plus the matches for the without current characters
   7. Time complexity O\(mn\)
   8. Space complexity O\(mn\)
2. asd

## Solution

```java
class Solution {
    public int numDistinct(String s, String t) {
        int m = t.length(), n = s.length();
        int[][] dp = new int[m + 1][n + 1];
        for (int j = 0; j <= n; j++) dp[0][j] = 1;
        for (int i = 1; i <= m; i++) {
            for (int j = 1; j <= n; j++) {
                dp[i][j] = dp[i][j - 1];
                if (s.charAt(j - 1) == t.charAt(i - 1)) dp[i][j] += dp[i - 1][j - 1];
            }
        }
        return dp[m][n];
    }
}
```

```java
class Solution {
    public int numDistinct(String s, String t) {
        int m = s.length(), n = t.length();
        int[] dp = new int[n + 1];
        dp[0] = 1;
        for (int i = 1; i <= m; i++) {
            int topLeft = dp[0];
            for (int j = 1; j <= n; j++) {
                int tmp = dp[j];
                if (s.charAt(i - 1) == t.charAt(j - 1)) dp[j] += topLeft;
                topLeft = tmp;
            }
        }
        return dp[n];
    }
}
```

## Additional {#additional}


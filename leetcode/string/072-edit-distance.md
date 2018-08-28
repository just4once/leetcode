# 072-edit-distance

## Question {#question}

[https://leetcode.com/problems/edit-distance/description/](https://leetcode.com/problems/edit-distance/description/)

Given two wordsword1andword2, find the minimum number of steps required to convertword1toword2. \(each operation is counted as 1 step.\)

You have the following 3 operations permitted on a word:

a\) Insert a character  
b\) Delete a character  
c\) Replace a character

**Example:**

```text

```

## Thought Process {#thought-process}

1. Dynamic Programing
   1. Create two dimensional array, dp, where dp\[i\]\[j\] store the minimum steps require for converting w1's 0th to ith character to w2's 0th to jth character
   2. If the characters match, we can use dp\[i - 1\]\[j - 1\]
   3. If the characters mismatch, we then need to check three options: replacing, inserting or deleting which are dp\[i - 1\]\[j - 1\], dp\[i-1\]\[j\] and dp\[i\]\[j - 1\] and then add 1, and these three values corresponds to minimum step for replacing i to j, deleting ith character from w1 and inserting the jth character from w2
   4. Time complexity O\(mn\)
   5. Space complexity O\(mn\)
2. Dynamic Programing - Space Reduction
   1. Time complexity O\(mn\)
   2. Space complexity O\(n\)

## Solution

```java
class Solution {
    public int minDistance(String word1, String word2) {
        int m = word1.length(), n = word2.length();
        char[] w1 = word1.toCharArray(), w2 = word2.toCharArray();
        int[][] dp = new int[m + 1][n + 1];
        for (int i = 1; i <= m; i++) dp[i][0] = i;
        for (int j = 1; j <= n; j++) dp[0][j] = j;
        for (int i = 1; i <= m; i++) {
            for (int j = 1; j <= n; j++) {
                if (w1[i - 1] == w2[j - 1]) dp[i][j] = dp[i - 1][j - 1];
                else dp[i][j] = Math.min(dp[i - 1][j - 1], Math.min(dp[i -1][j], dp[i][j - 1])) + 1;
            }
        }
        return dp[m][n];
    }
}
```

```java
class Solution {
    public int minDistance(String word1, String word2) {
        if (word1.length() < word2.length()) return minDistance(word2, word1);
        int m = word1.length(), n = word2.length();
        char[] w1 = word1.toCharArray(), w2 = word2.toCharArray();
        int[] dp = new int[n + 1];
        for (int j = 1; j <= n; j++) dp[j] = j;
        for (int i = 1; i <= m; i++) {
            int pre = i, cur = 0;
            for (int j = 1; j <= n; j++) {
                if (w1[i - 1] == w2[j - 1]) cur = dp[j - 1];
                else cur = Math.min(pre, Math.min(dp[j - 1], dp[j])) + 1;
                dp[j - 1] = pre;
                pre = cur;
            }
            dp[n] = pre;
        }
        return dp[n];
    }
}
```

## Additional {#additional}


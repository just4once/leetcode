### Question {#question}

[https://leetcode.com/problems/wildcard-matching/description/](https://leetcode.com/problems/wildcard-matching/description/)

Implement wildcard pattern matching with support for '?' and '\*'.

**Example:**

```
'?' Matches any single character.
'*' Matches any sequence of characters (including the empty sequence).

The matching should cover the entire input string (not partial).

The function prototype should be:
bool isMatch(const char *s, const char *p)

Some examples:
isMatch("aa","a") → false
isMatch("aa","aa") → true
isMatch("aaa","aa") → false
isMatch("aa", "*") → true
isMatch("aa", "a*") → true
isMatch("ab", "?*") → true
isMatch("aab", "c*a*b") → false
```

### Thought Process {#thought-process}

1. DP
   1. Similar to [010-Regular Expression Matching](/leetcode/string/010-regular-expression-matching.md), we create two dimensional array to store the match result
   2. dp\[i\]\[j\] store the match result for 0th to ith character from s and 0th to jth character from p
   3. Time complexity O\(sp\)
   4. Space complexity O\(sp\)
2. Two Pointers
   1. We use two pointers to point to the location of s and p
   2. And another two to save the location of visiting character from s and \* from j
   3. Anytime we have mismatch, we go back and check if we have seen \* before and soak up as many bad character as possible
   4. At the end, we just check if the remaining p character is \*

### Solution

```java
class Solution {
    public boolean isMatch(String s, String p) {
        char[] S = s.toCharArray(), P = p.toCharArray();
        boolean[][] dp = new boolean[s.length() + 1][p.length() + 1];
        dp[0][0] = true;
        for (int j = 0; j < P.length && P[j] == '*'; j++) {
            dp[0][j + 1] = true;
        }
        for (int i = 0; i < S.length; i++) {
            for (int j = 0; j < P.length; j++) {
                // we can either ignore s's character dp[i - 1][j] or
                // treat * as empty using dp[i][j - 1]
                if (P[j] == '*') {
                    dp[i + 1][j + 1] = dp[i][j + 1] || dp[i + 1][j];
                } else {
                    dp[i + 1][j + 1] = dp[i][j] && (S[i] == P[j] || P[j] == '?');
                }
            }
        }
        return dp[S.length][P.length];
    }
}
```

```java
class Solution {
    public boolean isMatch(String s, String p) {
        int i = 0, j = 0;
        int star = -1, mark = -1;
        while (i < s.length()) {
            if (j < p.length() && (s.charAt(i) == p.charAt(j) || p.charAt(j) == '?')) {
                i++;
                j++;
            } else if (j < p.length() && p.charAt(j) == '*') {
                mark = i;
                star = j;
                j++;
            } else if (star != -1) {
                i = ++mark;
                j = star + 1;
            } else {
                return false;
            }
        }
        while (j < p.length() && p.charAt(j) == '*') j++;
        return j == p.length();
    }
}
```

### Additional {#additional}




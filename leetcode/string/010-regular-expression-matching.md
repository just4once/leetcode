### Question {#question}

[https://leetcode.com/problems/regular-expression-matching/description/](https://leetcode.com/problems/regular-expression-matching/description/)

Implement regular expression matching with support for '.' and '\*'.

**Example:**

```
'.' Matches any single character.
'*' Matches zero or more of the preceding element.

The matching should cover the entire input string (not partial).

The function prototype should be:
bool isMatch(const char *s, const char *p)

Some examples:
isMatch("aa","a") → false
isMatch("aa","aa") → true
isMatch("aaa","aa") → false
isMatch("aa", "a*") → true
isMatch("aa", ".*") → true
isMatch("ab", ".*") → true
isMatch("aab", "c*a*b") → true
```

### Thought Process {#thought-process}

1. Recursion
   1. We check the first characters matched by s\[0\] == p\[0\] or p\[0\] == '.'
   2. If the second character is \*, then there are two cases
      1. We ignore the whether first character matches or not, we just start from index 2 and match rest
      2. We can check first character match and matches next character
   3. If first character match, we check next character with next character from pattern
   4. Time complexity O\(\(T+P\)2^\(T+P/2\)\)
   5. Space complexity O\(T + P/2\) due to stack
2. Dynamic Programing \(Top Down with Memo\)
   1. Create memoization array to store the match result for s\[i:\] to p\[j:\]
   2. This avoid the expensive recalculation of subproblem
   3. Time complexity O\(TP\)
   4. Space complexity O\(TP\)
3. Dynamic Programing \(Bottom up\)
   1. Same as before
   2. Time complexity O\(TP\)
   3. Space complexity O\(TP\)

### Solution

```java
class Solution {
    public boolean isMatch(String s, String p) {
        return isMatch(s.toCharArray(), 0, p.toCharArray(), 0);
    }

    private boolean isMatch(char[] s, int i, char[] p, int j) {
        if (j == p.length) return i == s.length;
        boolean firstMatch = i != s.length && (s[i] == p[j] || p[j] == '.');
        if (j + 1 < p.length && p[j + 1] == '*') {
            return isMatch(s, i, p, j + 2) || (firstMatch && isMatch(s, i + 1, p, j));
        } else {
            return firstMatch && isMatch(s, i + 1, p, j + 1);
        }
    }
}
```

```java
class Solution {
    public boolean isMatch(String s, String p) {
        Boolean[][] memo = new Boolean[s.length() + 1][p.length() + 1];
        return isMatch(s.toCharArray(), 0, p.toCharArray(), 0, memo);
    }

    private boolean isMatch(char[] s, int i, char[] p, int j, Boolean[][] memo) {
        if (memo[i][j] != null) return memo[i][j];
        boolean res = false;
        if (j == p.length) {
            res = i == s.length;
        } else {
            boolean firstMatch = i < s.length && (s[i] == p[j] || p[j] == '.');
            if (j + 1 < p.length && p[j + 1] == '*') {
                res = isMatch(s, i, p, j + 2, memo) || (firstMatch && isMatch(s, i + 1, p, j, memo));
            } else {
                res = firstMatch && isMatch(s, i + 1, p, j + 1, memo);
            }
        }
        memo[i][j] = res;
        return res;
    }
}
```

```java
class Solution {
    public boolean isMatch(String s, String p) {
        boolean[][] dp = new boolean[s.length() + 1][p.length() + 1];
        dp[s.length()][p.length()] = true;
        char[] S = s.toCharArray(), P = p.toCharArray();
        for (int i = s.length(); i >= 0; i--) {
            for (int j = p.length() - 1; j >= 0; j--) {
                boolean firstMatch = i < s.length() && (S[i] == P[j] || P[j] == '.');
                if (j + 1 < p.length() && P[j + 1] == '*') {
                    dp[i][j] = dp[i][j + 2] || (firstMatch && dp[i + 1][j]);
                } else {
                    dp[i][j] = firstMatch && dp[i + 1][j + 1];
                }
            }
        }
        return dp[0][0];
    }
}
```

```java
class Solution {
    public boolean isMatch(String s, String p) {
        boolean[][] dp = new boolean[s.length() + 1][p.length() + 1];
        dp[0][0] = true;
        char[] S = s.toCharArray(), P = p.toCharArray();
        for (int j = 1; j < p.length(); j++) {
            if (P[j] == '*' && dp[0][j - 1]) dp[0][j + 1] = true;
        }
        for (int i = 0; i < s.length(); i++) {
            for (int j = 0; j < p.length(); j++) {
                // if they are same, we can use i - 1 and j - 1 result
                if (S[i] == P[j] || P[j] == '.') dp[i + 1][j + 1] = dp[i][j];
                // if cur pattern is *, we can check whether the previous character
                // matches or not
                else if (P[j] == '*') {
                    // not use it
                    dp[i + 1][j + 1] = dp[i + 1][j - 1];
                    if (S[i] == P[j - 1] || P[j - 1] == '.') {
                        dp[i + 1][j + 1] |= dp[i][j + 1];
                    }
                }
            }
        }
        return dp[s.length()][p.length()];
    }
}
```

### Additional {#additional}




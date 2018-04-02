### Question {#question}

[https://leetcode.com/problemset/all/?topicSlugs=string](https://leetcode.com/problemset/all/?topicSlugs=string)

Given a string s, find the longest palindromic substring in s. You may assume that the maximum length of s is 1000.

**Example 1:**

```
Input: "babad"

Output: "bab"

Note: "aba" is also a valid answer.
```

**Example 2:**

```
Input: "cbbd"

Output: "bb"
```

### Thought Process {#thought-process}

1. Expand at Center
   1. At each index, we try to use the character as center or the character and its left character as center
   2. We try to expand as much as possible, and then return the length
   3. Time complexity O\(n^2\)
   4. Space complexity O\(1\)
2. Manacher
   1. By padding string with \# in between characters, we can see that every position becomes a potential palindromic center
   2. For example, S = “abaaba”, T = “\#a\#b\#a\#a\#b\#a\#”
   3. As we expand around each position, we store intermediate result in a dp array, where dp\[i\] indicates the length of palindrome centers at Ti
   4. Due to palindromic property, we save the computation for next elements by using it mirrored counterpart. However if the mirrored counterpart's dp\[i'\] expand outside of boundary
   5. if dp\[i'\] &lt;= R - i, then dp\[i\] = dp\[i'\], else dp\[i\] &gt;= dp\[i'\] \(we need to expand and check\)
   6. [https://articles.leetcode.com/longest-palindromic-substring-part-ii/](https://articles.leetcode.com/longest-palindromic-substring-part-ii/)
   7. Time complexity O\(n\)
   8. Space complexity O\(n\)

### Solution

```java
class Solution {
    public String longestPalindrome(String s) {
        int len = 0, start = 0;
        char[] chars = s.toCharArray();
        for (int i = 0; i < s.length(); i++) {
            int len1 = expand(chars, i, i);
            int len2 = expand(chars, i - 1, i);
            int tmp = Math.max(len1, len2);
            if (tmp > len) {
                start = i - tmp / 2;
                len = tmp;
            }
        }
        return s.substring(start, start + len);
    }
    
    private int expand(char[] chars, int i, int j) {
        while (i >= 0 && j < chars.length && chars[i] == chars[j]) {
            i--;
            j++;
        }
        return j - i - 1;
    }
}
```

```java
class Solution {
    public String longestPalindrome(String s) {
		char[] t = pad(s);
        int[] dp = expand(t);
        int len = 0, C = 0;
        for (int i = 1; i < dp.length - 1; i++) {
            if (dp[i] > len) {
                C = i;
                len = dp[i];
            }
        }
        return s.substring((C - 1 - len) / 2, (C - 1 + len) / 2);
    }
    
    private char[] pad(String s) {
        char[] chars = s.toCharArray();
        int n = chars.length;
        char[] res = new char[2 * n + 3];
        res[0] = '^';
        for (int i = 0; i < n; i++) {
            res[2 * i + 1] = '#';
            res[2 * i + 2] = chars[i];
        }
        res[2 * n + 1] = '#';
        res[2 * n + 2] = '$';
        return res;
    }
    
    private int[] expand(char[] t) {
        int C = 0, R = 0;
        int[] dp = new int[t.length];
        for (int i = 1; i < t.length - 1; i++) {
            int M = 2 * C - i; // C - (i - C)
            if (i < R) dp[i] = Math.min(dp[M], R - i);
            // expand i
            while (t[i - dp[i] - 1] == t[i + dp[i] + 1]) dp[i]++;
            if (i + dp[i] > R) {
                C = i;
                R = i + dp[i];
            }
        }
        return dp;
    }
}
```

### Additional {#additional}




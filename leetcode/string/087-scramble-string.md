### Question {#question}

[https://leetcode.com/problems/scramble-string/description/](https://leetcode.com/problems/scramble-string/description/)

Given a string s1, we may represent it as a binary tree by partitioning it to two non-empty substrings recursively.

**Example:**

Below is one possible representation of s1 = "**great**":

```
    great
   /    \
  gr    eat
 / \    /  \
g   r  e   at
           / \
          a   t
```

To scramble the string, we may choose any non-leaf node and swap its two children.

For example, if we choose the node "**gr**" and swap its two children, it produces a scrambled string "**rgeat**".

We say that "**rgeat**" is a scrambled string of "**great**".

```
    rgeat
   /    \
  rg    eat
 / \    /  \
r   g  e   at
           / \
          a   t
```

Similarly, if we continue to swap the children of nodes "**eat**" and "**at**", it produces a scrambled string "**rgtae**".

We say that "**rgtae**" is a scrambled string of "**great**".

```
    rgtae
   /    \
  rg    tae
 / \    /  \
r   g  ta  e
       / \
      t   a
```

### Thought Process {#thought-process}

1. Recursion
   1. If the string lengths do not equal or the characters are mismatch \(use map\), we can return false
   2. Since each part can be scrambled, we need recursion to check both scrambleness of left part and right part
   3. Also because we swap the text, the match for left could also happen on the right side, we need to check the match between left and right as well
   4. Time complexity O\(2^n\)
   5. Space complexity O\(n\) due to recursion stack
2. Recursion with Rolling Hash
   1. Use prime number to facilitate the process of determine the left part and right part equivalence
   2. We check the scrambless only if the left hash of s1 match with left hash of s2 or right hash of s2
   3. Time complexity O\(2^n\)
   4. Space complexity O\(n\) due to recursion
3. Bottom Up DP
   1. We create three dimensional array, dp\[\]\[\]\[\], where dp\[i\]\[j\]\[k\] indicate the scrambleness of length i and jth character from s1 and kth character from s2
   2. We need to check every possible breaking point from 1 to i - 1 using a variable b
   3. There are two ways to check the scrambleness
      1. Left part match left part, and right part match right part, so we check match from j and k with length b, and match from j + b and k + b with length i - b
      2. Left part match right part, and right part match left part, so we check match from j and k + i - b with length b, and match from j + b and k for length i - b
   4. Time complexity O\(n^4\)
   5. Space complexity O\(n^3\)

### Solution

```java
class Solution {
    public boolean isScramble(String s1, String s2) {
        if (s1.length() != s2.length()) return false;
        if (s1.equals(s2)) return true;
        int[] map = new int[26];
        int n = s1.length();
        for (int i = 0; i < n; i++) {
            map[s1.charAt(i) - 'a']++;
            map[s2.charAt(i) - 'a']--;
        }
        for (int i = 0; i < 26; i++) {
            if (map[i] != 0) return false;
        }
        // set the breaker point
        for (int i = 1; i < n; i++) {
            if (isScramble(s1.substring(0, i), s2.substring(0, i)) && isScramble(s1.substring(i), s2.substring(i))) return true;
            if (isScramble(s1.substring(0, i), s2.substring(n - i)) && isScramble(s1.substring(i), s2.substring(0, n - i))) return true;
        }
        return false;
    }
}
```

```java
class Solution {
    int[] p = {2, 3, 5, 7, 11, 13, 17, 19, 23, 29, 31, 37, 41, 43, 47, 53, 59, 61, 67, 71, 73, 79, 83, 89, 97, 101};
    public boolean isScramble(String s1, String s2) {
        if (s1.length() != s2.length()) return false;
        if (s1.length() <= 1) return s1.equals(s2);
        if (s1.equals(s2)) return true;
        // l1 is the left of s1, l2 is left of s2, r2 is right of s2
        // We use rolling hash to make sure that we have same char set.
        int n = s2.length();
        long l1 = p[s1.charAt(0) - 'a'], l2 = p[s2.charAt(0) - 'a'], r2 = p[s2.charAt(n - 1) - 'a'];
        for(int i = 1; i < n; i++){
            if(l1 == l2 && isScramble(s1.substring(0, i), s2.substring(0, i)) && isScramble(s1.substring(i), s2.substring(i))) return true;
            if(l1 == r2 && isScramble(s1.substring(0, i), s2.substring(n - i)) && isScramble(s1.substring(i), s2.substring(0, n - i))) return true;
            l1 *= p[s1.charAt(i) - 'a'];
            l2 *= p[s2.charAt(i) - 'a'];
            r2 *= p[s2.charAt(n - i - 1) - 'a'];
        }
        return false;
    }
}
```

```java
class Solution {
    public boolean isScramble(String s1, String s2) {
        if (s1.length() != s2.length()) return false;
        if (s1.equals(s2)) return true;
        int n = s1.length();
        boolean[][][] dp = new boolean[n + 1][n][n];
        char[] c1 = s1.toCharArray(), c2 = s2.toCharArray();
        // initialization for length = 1
        for (int j = 0; j < n; j++) {
            for (int k = 0; k < n; k++) {
                if (c1[j] == c2[k]) {
                    dp[1][j][k] = true;
                }
            }
        }
        // checking for length start from 2 to n
        for (int i = 2; i <= n; i++) {
            for (int j = 0; j <= n - i; j++) {
                for (int k = 0; k <= n - i; k++) {
                    //check every possible breaking point
                    for (int b = 1; b < i && !dp[i][j][k]; b++) {
                        dp[i][j][k] = (dp[b][j][k] && dp[i - b][j + b][k + b]) || (dp[b][j][k + i - b] && dp[i - b][j + b][k]);
                    }
                }
            }
        }
        return dp[n][0][0];
    }
}
```

### Additional {#additional}




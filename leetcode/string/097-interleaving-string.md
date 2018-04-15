### Question {#question}

[https://leetcode.com/problems/interleaving-string/description/](https://leetcode.com/problems/interleaving-string/description/)

Given s1, s2, s3, find whether s3 is formed by the interleaving of s1 and s2.

**Example:**

```
Given:
s1 = "aabcc",
s2 = "dbbca",

When s3 = "aadbbcbcac", return true.
When s3 = "aadbbbaccc", return false.
```

### Thought Process {#thought-process}

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
3. asd

### Solution

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



### Additional {#additional}




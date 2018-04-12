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
2. Recursion with Memo
3. Bottom Up DP
   1. We create three dimensional array, dp\[\]\[\]\[\], where dp\[i\]\[j\]\[k\] indicate the scrambleness of length i and jth character from s1 and kth character from s2
   2. We need to check every possible breaking point from 1 to i - 1 using a variable b
   3. There are two ways to check the scrambleness
      1. Match from i and j with length b, and match from i + b and j + b with length i - b
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

### Additional {#additional}




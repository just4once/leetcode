# 076-minimum-window-substring

## Question {#question}

[https://leetcode.com/problems/minimum-window-substring/description/](https://leetcode.com/problems/minimum-window-substring/description/)

Given a string S and a string T, find the minimum window in S which will contain all the characters in T in complexity O\(n\).

**Example:**

```text
S = "ADOBECODEBANC"
T = "ABC"
Minimum window is "BANC".
```

## Thought Process {#thought-process}

1. Brute Force
   1. Try every possible subsequence
   2. Time complexity O\(n^2\)
   3. Space complexity O\(1\)
2. Sliding Window
   1. Two pointers to track the start and end point of our window
   2. Once we have include all the letter, we start shrinking the start pointers
   3. Time complexity O\(n\)
   4. Space complexity O\(1\)

## Solution

```java
class Solution {
    public String minWindow(String s, String t) {
        if (t.length() > s.length()) return "";
        int[] counts = new int[256];
        for (char c : t.toCharArray()) {
            counts[c]++;
        }
        int left = 0, right = 0, n = t.length(), start = 0, len = Integer.MAX_VALUE;
        char[] chars = s.toCharArray();
        while (right < s.length()) {
            if (counts[chars[right++]]-- > 0) n--;
            while (n == 0) {
                if (right - left < len) {
                    start = left;
                    len = right - left;
                } 
                if (counts[chars[left++]]++ >= 0) n++;
            }
        }
        len = len == Integer.MAX_VALUE ? 0 : len;
        return s.substring(start, start + len);
    }
}
```

## Additional {#additional}


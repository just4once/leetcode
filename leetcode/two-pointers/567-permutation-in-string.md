# 567-permutation-in-string

## Question {#question}

[https://leetcode.com/problems/permutation-in-string/description/](https://leetcode.com/problems/permutation-in-string/description/)

Given two strings s1 and s2, write a function to return true if s2 contains the permutation of s1. In other words, one of the first string's permutations is the substring of the second string.

**Example:**

```text
Input:s1 = "ab" s2 = "eidbaooo"
Output:True
Explanation: s2 contains one permutation of s1 ("ba").
```

```text
Input:s1= "ab" s2 = "eidboaoo"
Output: False
```

## Thought Process {#thought-process}

1. Two Pointers
   1. Scanning left to right with sliding window
   2. When all the characters from s1 are used up, we have to make sure the sliding window is exactly the length of s1
   3. Time complexity O\(n\)
   4. Space complexity O\(

## Solution

```java
class Solution {
    public boolean checkInclusion(String s1, String s2) {
        int[] map = new int[128];
        for (char c : s1.toCharArray()) {
            map[c]++;
        }
        int count = s1.length();
        char[] chars = s2.toCharArray();
        int left = 0, right = 0;
        while (right < chars.length) {
            if (map[chars[right++]]-- > 0) count--;
            while (count == 0) {
                if (right - left == s1.length()) return true;
                if (++map[chars[left++]] > 0) count++;
            }
        }
        return false;
    }
}
```

## Additional {#additional}


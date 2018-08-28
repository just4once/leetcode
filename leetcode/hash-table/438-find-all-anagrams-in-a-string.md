# 438-find-all-anagrams-in-a-string

## Question {#question}

[https://leetcode.com/problems/find-all-anagrams-in-a-string/description/](https://leetcode.com/problems/find-all-anagrams-in-a-string/description/)

Given a string **s** and a **non-empty** string **p**, find all the start indices of **p**'s anagrams in **s**.

Strings consists of lowercase English letters only and the length of both strings **s** and **p**will not be larger than 20,100.

The order of output does not matter.

**Example 1:**

```text
Input:
s: "cbaebabacd" p: "abc"

Output:
[0, 6]

Explanation:
The substring with start index = 0 is "cba", which is an anagram of "abc".
The substring with start index = 6 is "bac", which is an anagram of "abc".
```

**Example 2:**

```text
Input:
s: "abab" p: "ab"

Output:
[0, 1, 2]

Explanation:
The substring with start index = 0 is "ab", which is an anagram of "ab".
The substring with start index = 1 is "ba", which is an anagram of "ab".
The substring with start index = 2 is "ab", which is an anagram of "ab".
```

## Thought Process {#thought-process}

1. Map - Sliding Window
   1. Use map to record the count and left and right pointers to track the windows
   2. Time complexity O\(n\)
   3. Space complexity O\(n\) or O\(1\)

## Solution

```java
class Solution {
    public List<Integer> findAnagrams(String s, String p) {
        List<Integer> res = new ArrayList<>();
        if (s.length() < p.length()) return res;
        int[] map = new int[128];
        for (char c : p.toCharArray()) {
            map[c]++;
        }
        // two pointers to track the window
        int left = 0, right = 0;
        char[] chars = s.toCharArray();
        int m = s.length(), n = p.length(), count = n;
        while (right < m) {
            if (map[chars[right++]]-- > 0) count--;
            if (count == 0) res.add(left);
            if (right - left == n && map[chars[left++]]++ >= 0) count++;
        }
        return res;
    }
}
```

## Additional {#additional}


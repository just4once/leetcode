# 003-longest-substring-without-repeating-characters

## Question {#question}

[https://leetcode.com/problems/longest-substring-without-repeating-characters/description/](https://leetcode.com/problems/longest-substring-without-repeating-characters/description/)

Given a string, find the length of the **longest substring** without repeating characters.

**Example:**

```text
Given "abcabcbb", the answer is "abc", which the length is 3.

Given "bbbbb", the answer is "b", with the length of 1.

Given "pwwkew", the answer is "wke", with the length of 3. Note that the answer must be a substring, "pwke" is a subsequence and not a substring.
```

## Thought Process {#thought-process}

1. Brute Force
   1. We can try each find the longest substring starting with every element
   2. Time complexity O\(n^2\)
   3. Space complexity O\(1\)
2. Hash Table - Sliding Windows
   1. We use the set to track if we have added this character before
   2. If we can't add the current character, we need to make sure all the characters before the previous occurrence \(as well as itself\) are deleted before we starting a new sequence
   3. Time complexity O\(n\)
   4. Space complexity O\(n\)
3. Hash Table - Optimized
   1. From the above observation, we can see that we can directly jump the index to the index right after the the previous occurrence
   2. Time complexity O\(n\)
   3. Space complexity O\(n\) or O\(1\) if use int array

## Solution

1. Hash Table

```java
class Solution {
    public int lengthOfLongestSubstring(String s) {
        Set<Character> set = new HashSet<>();
        int i = 0, j = 0, len = 0, n = s.length();
        while (i < n && j < n) {
            if (set.add(s.charAt(j))) {
                set.add(s.charAt(j++));
                len = Math.max(len, j - i);
            } else {
                set.remove(s.charAt(i++));
            }
        }
        return len;
    }
}
```

1. HashTable

```java
class Solution {
    public int lengthOfLongestSubstring(String s) {
        Map<Character, Integer> map = new HashMap<>();
        int left = 0, len = 0;
        for (int right = 0; right < s.length(); right++) {
            char c = s.charAt(right);
            left = Math.max(left, map.getOrDefault(c, left - 1) + 1);
            map.put(c, right);
            len = Math.max(right - left + 1, len);
        }
        return len;
    }
}
```

Or save the next index to facilitate the computation

```java
class Solution {
    public int lengthOfLongestSubstring(String s) {
        Map<Character, Integer> map = new HashMap<>();
        int left = 0, len = 0;
        for (int right = 0; right < s.length(); right++) {
            char c = s.charAt(right);
            left = Math.max(left, map.getOrDefault(c, left));
            map.put(c, right + 1);
            len = Math.max(right - left + 1, len);
        }
        return len;
    }
}
```

Use int array as Map

```java
class Solution {
    public int lengthOfLongestSubstring(String s) {
        int R = 128;
        int[] map = new int[R];
        int left = 0, len = 0;
        for (int right = 0; right < s.length(); right++) {
            char c = s.charAt(right);
            left = Math.max(left, map[c]);
            map[c] = right + 1;
            len = Math.max(right - left + 1, len);
        }
        return len;
    }
}
```

## Additional {#additional}


### Question {#question}

[https://leetcode.com/problems/valid-anagram/description/](https://leetcode.com/problems/valid-anagram/description/)

Given two strings s and t, write a function to determine if t is an anagram of s.

**Example:**

```
s = "anagram", t = "nagaram", return true.
s = "rat", t = "car", return false.
```

### Thought Process {#thought-process}

1. Hash Table
   1. Store the frequency in the map
   2. If the count reach 0 when encounter a particular character, we know we don't have enough character from the String s
   3. Time complexity O\(n\)
   4. Space complexity O\(1\), at most 256

### Solution

```java
class Solution {
    public boolean isAnagram(String s, String t) {
        if (s.length() != t.length()) return false;
        char[] map = new char[256];
        for (char c : s.toCharArray()) {
            map[c]++;
        }
        for (char c: t.toCharArray()) {
            if (map[c] == 0) return false;
            map[c]--;
        }
        return true;
    }
}
```

### Additional {#additional}




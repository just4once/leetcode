### Question {#question}

[https://leetcode.com/problems/isomorphic-strings/description/](https://leetcode.com/problems/isomorphic-strings/description/)

Given two strings **s **and **t**, determine if they are isomorphic.

Two strings are isomorphic if the characters in **s **can be replaced to get **t**.

All occurrences of a character must be replaced with another character while preserving the order of characters. No two characters may map to the same character but a character may map to itself.

**Example:**

```
Given "egg", "add", return true.

Given "foo", "bar", return false.

Given "paper", "title", return true.
```

### Thought Process {#thought-process}

1. Hash Table and Boolean
   1. Use hashtable to track the mapping of characters and boolean to track whether a character has been used already
   2. Time complexity O\(n\)
   3. Space complexity O\(1\)

### Solution

```java
class Solution {
    public boolean isIsomorphic(String s, String t) {
        if (s.length() != t.length()) return false;
        char[] map = new char[256];
        boolean[] used = new boolean[256];
        char[] sc = s.toCharArray();
        char[] tc = t.toCharArray();
        for (int i = 0; i < sc.length; i++) {
            // if this character has not been mapped
            if (map[sc[i]] == 0) {
                if (used[tc[i]]) return false;
                map[sc[i]] = tc[i];
                used[tc[i]] = true;
            } else if (map[sc[i]] != tc[i]) {
                return false;
            }
        }
        return true;
    }
}
```

### Additional {#additional}




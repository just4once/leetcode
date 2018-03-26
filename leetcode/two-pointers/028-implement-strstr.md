### Question {#question}

[https://leetcode.com/problems/implement-strstr/description/](https://leetcode.com/problems/implement-strstr/description/)

Implement [strStr\(\)](http://www.cplusplus.com/reference/cstring/strstr/).

Return the index of the first occurrence of needle in haystack, or **-1 **if needle is not part of haystack.

**Example:**

```
Input: haystack = "hello", needle = "ll"
Output: 2

Input: haystack = "aaaaa", needle = "bba"
Output: -1
```

### Thought Process {#thought-process}

1. Two Pointers
   1. At each position, we simply compare the letter matches
   2. Time complexity O\(hn\), where h is the length of haystack and n is length of needle
   3. Space complexity O\(1\)

### Solution

```java
class Solution {
    public int strStr(String haystack, String needle) {
        if(haystack.length() < needle.length()) return -1;
        if(needle.length() == 0) return 0;
        char[] hc = haystack.toCharArray();
        char[] nc = needle.toCharArray();
        int id = -1;
        for(int i = 0; i <= hc.length - nc.length; i++){
            if(match(hc, i, nc)){
                return i;
            }
        }
        return id;
    }
    
    public boolean match(char[] hc, int start, char[] nc){
        for(int i = 0; i < nc.length; i++){
            if(hc[start++] != nc[i]) return false;
        }
        return true;
    }
}
```

### Additional {#additional}




# 014-longest-common-prefix

## Question {#question}

[https://leetcode.com/problems/longest-common-prefix/description/](https://leetcode.com/problems/longest-common-prefix/description/)

Write a function to find the longest common prefix string amongst an array of strings.

**Example:**

```text

```

## Thought Process {#thought-process}

1. Horizontal Scanning
   1. Use first string as basis, then loop through all the other string
   2. At any index if the character is not matched, we return the last length
   3. Time complexity O\(S\), where S is total length of all strings
   4. Space complexity O\(1\)
2. Vertical Scanning
   1. Scan all the letter from same index, return last level immediately if any character mismatch
   2. Time complexity O\(S\)
   3. Space complexity O\(1\)
3. Divide and Conquer
   1. Divide the string to left part and right part
   2. The LCP\(All\) = LCP\(LCP\(Left\), LCP\(Right\)\)
   3. Time complexity\(S\)
   4. Space complexity O\(m logn\) where m is length and n is number of string
4. Trie
   1. Build Trie tree, and then search deep to the level until the child node is more than 1
   2. Time complexity O\(m\), where m is length of word, building trie takes O\(S\) times
   3. Space complexity O\(S\)

## Solution

```java
class Solution {    
    public String longestCommonPrefix(String[] strs) {
        if(strs == null || strs.length == 0) return "";
        String prefix = strs[0];
        for (int i = 1; i < strs.length; i++) {
            while (strs[i].indexOf(prefix) != 0) {
                prefix = prefix.substring(0, prefix.length() - 1);
                if (prefix.isEmpty()) break;
            }
        }
        return prefix;
    }
}
```

```java
class Solution {    
    public String longestCommonPrefix(String[] strs) {
        if(strs == null || strs.length == 0) return "";
        String prefix = strs[0];
        for (int i = 0; i < prefix.length(); i++) {
            char c = prefix.charAt(i);
            for (int j = 1; j < strs.length; j++) {
                if (strs[j].length() == i || strs[j].charAt(i) != c) {
                    prefix = prefix.substring(0, i);
                    break;
                }
            }
        }
        return prefix;
    }
}
```

```java
class Solution {    
    public String longestCommonPrefix(String[] strs) {
        if(strs == null || strs.length == 0) return "";
        return longestCommonPrefix(strs, 0, strs.length - 1);
    }

    private String longestCommonPrefix(String[] strs, int i, int j) {
        if (i == j) return strs[i];
        else {
            int m = i + (j - i) / 2;
            String left = longestCommonPrefix(strs, i, m);
            String right = longestCommonPrefix(strs, m + 1, j);
            return common(left, right);
        }
    }

    private String common(String left, String right) {
        int n = Math.min(left.length(), right.length());
        int i = 0;
        while (i < n) {
            if (left.charAt(i) != right.charAt(i)) {
                break;
            }
            i++;
        }
        return left.substring(0, i);
    }
}
```

## Additional {#additional}


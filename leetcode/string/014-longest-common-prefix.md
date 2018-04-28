### Question {#question}

[https://leetcode.com/problems/longest-common-prefix/description/](https://leetcode.com/problems/longest-common-prefix/description/)

Write a function to find the longest common prefix string amongst an array of strings.

**Example:**

```

```

### Thought Process {#thought-process}

1. Horizontal Scanning
   1. Use first string as basis, then loop through all the other string
   2. At any index if the character is not matched, we return the last length
   3. Time complexity O\(S\), where S is total length of all strings
   4. Space complexity O\(1\)
2. Vertical Scanning
   1. Scan all the letter from same index, return last level immediately if any character mismatch
   2. Time complexity O\(S\)
   3. Space complexity O\(1\)
3.Divide and Conquer
   1. Divide the string to left part and right part
   2. The LCP\(All\) = LCP\(LCP\(Left\), LCP\(Right\)\)
   3. Time complexity\(S\)
   4. Space complexity O\(m logn\) where m is length and n is number of string
4. Trie
   1. Build Trie tree, and then search deep to the level until the child node is more than 1
   2. Time complexity O\(m\), where m is length of word, building trie takes O\(S\) times
   3. Space complexity O\(S\)

### Solution

```java

```

### Additional {#additional}




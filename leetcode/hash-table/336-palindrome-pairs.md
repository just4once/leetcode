### Question {#question}

Given a list of unique words, find all pairs of distinct indices \(i, j\) in the given list, so that the concatenation of the two words, i.e. words\[i\] + words\[j\] is a palindrome.

**Example:**

```
Given words = ["bat", "tab", "cat"]
Return [[0, 1], [1, 0]]
The palindromes are ["battab", "tabbat"]

Given words = ["abcd", "dcba", "lls", "s", "sssll"]
Return [[0, 1], [1, 0], [3, 2], [2, 4]]
The palindromes are ["dcbaabcd", "abcddcba", "slls", "llssssll"]
```

### Thought Process {#thought-process}

1. Brute Force
   1. Simply compare two strings can form a palindrome
   2. Time complexity O\(n^2w\), where n is length of list and w is the average length of word
   3. Space complexity O\(1\)
2. Hash Table
   1. Use hashmap to store the string and its index in the map
   2. We need to split the word into two parts at each index and check if there is reversed counter part
      1. if p1 is palindrome, we check if there exists reverse of p2 that we can append in the front
      2. or p2 is palindrome, we check if there exists reverse of p1 that we can append in the end
   3. Corner case is when there is empty string, we need to add all the strings that are palindrome
   4. Time complexity O\(nw^2\)
   5. Space complexity O\(n\)
3. asd

### Solution

```java

```

### Additional {#additional}




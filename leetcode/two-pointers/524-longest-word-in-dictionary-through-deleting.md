# 524-longest-word-in-dictionary-through-deleting

## Question {#question}

[https://leetcode.com/problems/longest-word-in-dictionary-through-deleting/description/](https://leetcode.com/problems/longest-word-in-dictionary-through-deleting/description/)

Given a string and a string dictionary, find the longest string in the dictionary that can be formed by deleting some characters of the given string. If there are more than one possible results, return the longest word with the smallest lexicographical order. If there is no possible result, return the empty string.

**Example 1:**

```text
Input:
s = "abpcplea", d = ["ale","apple","monkey","plea"]

Output: 
"apple"
```

**Example 2:**

```text
Input:
s = "abpcplea", d = ["a","b","c"]

Output: 
"a"
```

**Note:**

1. All the strings in the input will only contain lower-case letters.
2. The size of the dictionary won't exceed 1,000.
3. The length of all the strings in the input won't exceed 1,000.

## Thought Process {#thought-process}

1. String IndexOf function
   1. Use separate function to see if the letter can be found after its previous character
   2. Time complexity O\(nw\), where n is number of words, and w is width of the string
   3. Space complexity O\(1\)

## Solution

```java
class Solution {
    public String findLongestWord(String s, List<String> d) {
        String res = "";
        for (String word : d) {
            if (isSubsequence(word, s)) {
                if (word.length() > res.length()) res = word;
                else if (word.length() == res.length() && word.compareTo(res) < 0) res = word; 
            }
        }
        return res;
    }

    private boolean isSubsequence(String word, String longer) {
        if (word.length() > longer.length()) return false;
        int pos = 0;
        for (char c : word.toCharArray()) {
            pos = longer.indexOf(c, pos);
            if (pos == -1) return false;
            pos++;
        }
        return true;
    }
}
```

## Additional {#additional}


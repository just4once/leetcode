# 186-reverse-words-in-a-string-ii

## Question {#question}

[https://leetcode.com/problems/reverse-words-in-a-string-ii/description/](https://leetcode.com/problems/reverse-words-in-a-string-ii/description/)

Given an input string, reverse the string word by word. A word is defined as a sequence of non-space characters.

The input string does not contain leading or trailing spaces and the words are always separated by a single space.

**Example:**

```text
Given s = "the sky is blue",
return "blue is sky the".
```

Could you do it in-place without allocating extra space?

## Thought Process {#thought-process}

1. Reverse and Two Pointers
   1. We first reverse the whole string
   2. Then when we encounter a space, we reverse the start to the last position, so we "correct" the order
   3. Time complexity O\(n\)
   4. Space complexity O\(1\)

## Solution

```java
class Solution {
    public void reverseWords(char[] str) {
        int n = str.length;
        reverse(str, 0, n - 1);
        int start = 0, end = 0;
        while (end < n) {
            if (str[end] == ' ') {
                reverse(str, start, end - 1);
                start = end + 1;
            }
            end++;
        }
        reverse(str, start, end - 1);
    }

    private void reverse(char[] str, int i, int j) {
        while (i < j) {
            char tmp = str[i];
            str[i] = str[j];
            str[j] = tmp;
            i++;
            j--;
        }
    }
}
```

## Additional {#additional}


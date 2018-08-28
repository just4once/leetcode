# 058-length-of-last-word

## Question {#question}

[https://leetcode.com/problems/length-of-last-word/description/](https://leetcode.com/problems/length-of-last-word/description/)

Given a string s consists of upper/lower-case alphabets and empty space characters ' ', return the length of last word in the string.

If the last word does not exist, return 0.

**Note:**

A word is defined as a character sequence consists of non-space characters only.

**Example:**

```text
Input: "Hello World"
Output: 5
```

## Thought Process {#thought-process}

1. Scanning Backward
   1. Having a pointer points at the end of the string and move forward the string if it's a space
   2. Then we stop at the end of the last word
   3. Increase the length as long as the character is not a space
   4. Time complexity O\(n\)
   5. Space complexity O\(1\)

## Solution

```java
class Solution {
    public int lengthOfLastWord(String s) {
        int len = 0, tail = s.length() - 1;
        while(tail >= 0 && s.charAt(tail) == ' ') tail--;
        while(tail >= 0 && s.charAt(tail) != ' '){
            len++;
            tail--;
        }
        return len;
    }
}
```

## Additional {#additional}


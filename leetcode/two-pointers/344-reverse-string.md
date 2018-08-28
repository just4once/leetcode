# 344-reverse-string

## Question {#question}

[https://leetcode.com/problems/reverse-string/description/](https://leetcode.com/problems/reverse-string/description/)

Write a function that takes a string as input and returns the string reversed.

**Example:**

```text
Given s = "hello", return "olleh".
```

## Thought Process {#thought-process}

1. Two Pointers
   1. Use two pointer to track the start and end of string
   2. Swap the character at each pointer and then shrink toward the center
   3. Time complexity O\(n\)
   4. Space complexity O\(1\)

## Solution

```java
class Solution {
    public String reverseString(String s) {
        char[] chars = s.toCharArray();
        int i = 0, j = chars.length - 1;
        while (i < j) swap(chars, i++, j--);
        return String.valueOf(chars);
    }

    private void swap(char[] chars, int i, int j) {
        char tmp = chars[i];
        chars[i] = chars[j];
        chars[j] = tmp;
    }
}
```

## Additional {#additional}


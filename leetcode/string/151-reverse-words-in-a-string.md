# 151-reverse-words-in-a-string

## Question {#question}

[https://leetcode.com/problems/reverse-words-in-a-string/description/](https://leetcode.com/problems/reverse-words-in-a-string/description/)

Given an input string, reverse the string word by word.

**Example:**

```text
Given s = "the sky is blue",
return "blue is sky the".
```

## Thought Process {#thought-process}

1. Split by Space
   1. We can choose to trim the space or not, then we split by space
   2. Then start from the end of the string array, we start building word by word
   3. Time complexity O\(n\)
   4. Space complexity O\(n\)

## Solution

```java
public class Solution {
    public String reverseWords(String s) {
        String[] words = s.trim().split("\\s+");
        if (words.length == 0) return "";
        StringBuilder sb = new StringBuilder();
        for (int i = words.length - 1; i > 0; i--){
            sb.append(words[i]).append(" ");
        }
        sb.append(words[0]);
        return sb.toString();
    }
}
```

```java
public class Solution {
    public String reverseWords(String s) {
        String[] words = s.split(" ");
        StringBuilder sb = new StringBuilder();
        for (int i = words.length - 1; i >= 0; i--){
            if (words[i].length() > 0) sb.append(words[i]).append(" ");
        }
        if (sb.length() > 0) sb.setLength(sb.length() - 1);
        return sb.toString();
    }
}
```

## Additional {#additional}


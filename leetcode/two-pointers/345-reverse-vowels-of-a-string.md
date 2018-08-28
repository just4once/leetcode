# 345-reverse-vowels-of-a-string

## Question {#question}

[https://leetcode.com/problems/reverse-vowels-of-a-string/description/](https://leetcode.com/problems/reverse-vowels-of-a-string/description/)

Write a function that takes a string as input and reverse only the vowels of a string.

**Example:**

```text
Given s = "hello", return "holle".

Given s = "leetcode", return "leotcede".
```

## Thought Process {#thought-process}

1. Two Pointers
   1. Scan the first vowels from each side and then swap
   2. Time complexity O\(n\)
   3. Space complexity O\(1\)

## Solution

```java
class Solution {
    public String reverseVowels(String s) {
        if (s == null || s.length() <= 1) return s;
        Set<Character> vowels = new HashSet<>();
        vowels.add('a');
        vowels.add('e');
        vowels.add('i');
        vowels.add('o');
        vowels.add('u');
        vowels.add('A');
        vowels.add('E');
        vowels.add('I');
        vowels.add('O');
        vowels.add('U');
        char[] chars = s.toCharArray();
        int i = 0, j = chars.length - 1;
        while (i < j) {
            while (i < j && !vowels.contains(chars[i])) i++;
            while (i < j && !vowels.contains(chars[j])) j--;
            if (i >= j) break;
            char tmp = chars[i];
            chars[i] = chars[j];
            chars[j] = tmp;
            i++;
            j--;
        }
        return String.valueOf(chars);
    }
}
```

## Additional {#additional}


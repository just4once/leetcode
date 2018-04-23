### Question {#question}

[https://leetcode.com/problems/reverse-string/description/](https://leetcode.com/problems/reverse-string/description/)

Write a function that takes a string as input and returns the string reversed.

**Example:**

```
Given s = "hello", return "olleh".
```

### Thought Process {#thought-process}

1. Two Pointers
   1. Start from the ends of the string and swap the pair as we increment left pointer and decrement right pointer
   2. Time complexity O\(n\)
   3. Space complexity O\(1\)

### Solution

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

### Additional {#additional}




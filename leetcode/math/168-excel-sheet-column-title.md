### Question {#question}

[https://leetcode.com/problems/excel-sheet-column-title/description/](https://leetcode.com/problems/excel-sheet-column-title/description/)

Given a positive integer, return its corresponding column title as appear in an Excel sheet.

**Example:**

```
    1 -> A
    2 -> B
    3 -> C
    ...
    26 -> Z
    27 -> AA
    28 -> AB 
```

### Thought Process {#thought-process}

1. Mod
   1. Use character table to facilitate the process
   2. we need to use mod to get the correct character
   3. Time complexity O\(log n\)
   4. Space complexity O\(1\)

### Solution

```java
class Solution {
    private char[] table = new char []{'A','B','C','D','E','F','G','H','I','J','K','L','M','N','O','P','Q','R','S','T','U','V','W','X','Y','Z'};
    public String convertToTitle(int n) {
        StringBuilder sb = new StringBuilder();
        while (n > 0){
            sb.append(table[(n - 1) % 26]);
            n = (n - 1) / 26;
        }
        return sb.reverse().toString();
    }
}
```

### Additional {#additional}




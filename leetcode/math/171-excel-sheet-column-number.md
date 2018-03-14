### Question {#question}

[https://leetcode.com/problems/excel-sheet-column-number/description/](https://leetcode.com/problems/excel-sheet-column-number/description/)

Related to question [Excel Sheet Column Title](https://leetcode.com/problems/excel-sheet-column-title/)

Given a column title as appear in an Excel sheet, return its corresponding column number.

**Example:**

```
    A -> 1
    B -> 2
    C -> 3
    ...
    Z -> 26
    AA -> 27
    AB -> 28 
```

### Thought Process {#thought-process}

1. Reverse of Mod
   1. Just multiply and add
   2. Time complexity O\(n\)
   3. Space complexity O\(1\)

### Solution

```java
class Solution {
    public int titleToNumber(String s) {
        char[] chars = s.toCharArray();
        int res = 0;
        for (int i = 0; i < chars.length; i++){
            res = res * 26 + chars[i] - 'A' + 1;
        }
        return res;
    }
}
```

### Additional {#additional}




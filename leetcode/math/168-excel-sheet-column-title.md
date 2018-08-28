# 168-excel-sheet-column-title

## Question {#question}

[https://leetcode.com/problems/excel-sheet-column-title/description/](https://leetcode.com/problems/excel-sheet-column-title/description/)

Given a positive integer, return its corresponding column title as appear in an Excel sheet.

**Example:**

```text
    1 -> A
    2 -> B
    3 -> C
    ...
    26 -> Z
    27 -> AA
    28 -> AB
```

## Thought Process {#thought-process}

1. Mod
   1. we need to use mod to get the correct character
   2. Reverse the string at the end
   3. Time complexity O\(log n\)
   4. Space complexity O\(1\)

## Solution

```java
class Solution {
    public String convertToTitle(int n) {
        StringBuilder sb = new StringBuilder();
        while (n > 0){
            n--;
            sb.append((char)('A' + n % 26));
            n /= 26;
        }
        return sb.reverse().toString();
    }
}
```

## Additional {#additional}


### Question {#question}

[https://leetcode.com/problems/zigzag-conversion/description/](https://leetcode.com/problems/zigzag-conversion/description/)

The string "PAYPALISHIRING" is written in a zigzag pattern on a given number of rows like this: \(you may want to display this pattern in a fixed font for better legibility\)

**Example:**

```
P   A   H   N
A P L S I I G
Y   I   R

And then read line by line: "PAHNAPLSIIGYIR"
```

Write the code that will take a string and make this conversion given a number of rows:

convert\("PAYPALISHIRING", 3\) should return "PAHNAPLSIIGYIR".

### Thought Process {#thought-process}

1. Magic Number
   1. The first row and last row always insert next 2 \* num - 2th position, or referred as num in the code  \(excluding the character in the middle\)
   2. In the middle, we increase the next position by alternating between diff  and num - diff
   3. Time complexity O\(n\)
   4. Space complexity O\(n\)

### Solution

```java
class Solution {
    public String convert(String s, int numRows) {
        if(numRows==1) return s;
        char[] chars = s.toCharArray();
        int n = chars.length;
        StringBuilder sb = new StringBuilder();
        int num = numRows * 2 - 2;
        for(int i = 0; i < numRows; i++){
            int j = i;
            int diff = i * 2;
            while(j < n){
                sb.append(chars[j]);
                diff = (diff == num) ? num : num - diff; 
                j += diff;
            }
        }
        return sb.toString();
    }
}
```

### Additional {#additional}




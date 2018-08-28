# 012-integer-to-roman

## Question {#question}

[https://leetcode.com/problems/integer-to-roman/description/](https://leetcode.com/problems/integer-to-roman/description/)

Given an integer, convert it to a roman numeral.

Input is guaranteed to be within the range from 1 to 3999.

**Example:**

```text

```

## Thought Process {#thought-process}

1. Char Table and Int Table
   1. For every divisor, from 1000 to 1, we check the quotient and decide appropriate character to append
   2. Time complexity O\(n\), where n is number of divisor
   3. Space complexity O\(n\)
2. Char Table
   1. Time complexity O\(d\), where d is number of digits
   2. Space complexity O\(d\)

## Solution

```java
class Solution {
    public char[] createCharTable(){
        char[] table = new char[] {'M', 'D', 'C', 'L', 'X', 'V', 'I'};
        return table;
    }

    public int[] createIntTable(){
        int[] table = new int[] {1000, 500, 100, 50, 10, 5, 1};
        return table;
    }

    public String intToRoman(int num) {
        char[] charTable = createCharTable();
        int[] intTable = createIntTable();
        StringBuilder sb = new StringBuilder();
        for(int i = 0; i < intTable.length; i+=2){
            int k = num / intTable[i];
            if(k >= 10){
                return "";
            } else if (k == 9){
                sb.append(charTable[i]);
                sb.append(charTable[i-2]);
            } else if (k >= 5){
                sb.append(charTable[i-1]);
                for(int j = 5; j < k; j++) sb.append(charTable[i]);
            } else if (k == 4){
                sb.append(charTable[i]);
                sb.append(charTable[i-1]);
            } else {
                for(int j = 0; j < k; j++) sb.append(charTable[i]);
            }
            num %= intTable[i];
        }
        return sb.toString();
    }
}
```

```java
class Solution {
    public String intToRoman(int num) {
        String M[] = {"", "M", "MM", "MMM"};
        String C[] = {"", "C", "CC", "CCC", "CD", "D", "DC", "DCC", "DCCC", "CM"};
        String X[] = {"", "X", "XX", "XXX", "XL", "L", "LX", "LXX", "LXXX", "XC"};
        String I[] = {"", "I", "II", "III", "IV", "V", "VI", "VII", "VIII", "IX"};
        return M[num/1000] + C[(num%1000)/100] + X[(num%100)/10] + I[num%10];
    }
}
```

## Additional {#additional}


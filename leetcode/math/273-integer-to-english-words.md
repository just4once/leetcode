# 273-integer-to-english-words

## Question {#question}

[https://leetcode.com/problems/integer-to-english-words/description/](https://leetcode.com/problems/integer-to-english-words/description/)

Convert a non-negative integer to its english words representation. Given input is guaranteed to be less than 2^31 - 1.

**Example:**

```text
123 -> "One Hundred Twenty Three"
12345 -> "Twelve Thousand Three Hundred Forty Five"
1234567 -> "One Million Two Hundred Thirty Four Thousand Five Hundred Sixty Seven"
```

## Thought Process {#thought-process}

1. Divide by Different factor
   1. We simply compare the number with 1 billion, 1 million, 1 thousand, and 1
   2. If the number are greater we can append the respective string into the 

## Solution

```java
class Solution {
    private String[] single = {"", "One", "Two", "Three", "Four", "Five", "Six", "Seven", "Eight", "Nine", "Ten", "Eleven", "Twelve", "Thirteen", "Fourteen", "Fifteen", "Sixteen", "Seventeen", "Eighteen", "Nineteen"};
    private String[] ten = {"", "", "Twenty", "Thirty", "Forty", "Fifty", "Sixty", "Seventy", "Eighty", "Ninety"};

    public String numberToWords(int num) {
        if (num == 0) return "Zero";
        StringBuilder sb = new StringBuilder();
        int[] factors = {1000000000, 1000000, 1000, 1};
        String[] surfix = {" Billion ", " Million ", " Thousand ", " "};
        for (int i = 0; i < factors.length; i++) {
            if (num >= factors[i]) {
                sb.append(convert(num / factors[i])).append(surfix[i]);
                num %= factors[i];
            }
        }
        sb.setLength(sb.length() - 1);
        return sb.toString();
    }

    private String convert(int num) {
        if (num <= 0) return "";
        StringBuilder sb = new StringBuilder();
        if (num >= 100) {
            sb.append(single[num / 100]).append(" Hundred ");
            num %= 100;
        }
        if (num >= 20) {
            sb.append(ten[num / 10] + " ");
            num %= 10;
        }
        if (num > 0) {
            sb.append(single[num] + " ");
        }
        sb.setLength(sb.length() - 1);
        return sb.toString();
    }
}
```

## Additional {#additional}


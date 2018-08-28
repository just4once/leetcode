# 043-multiply-strings

## Question {#question}

[https://leetcode.com/problems/multiply-strings/description/](https://leetcode.com/problems/multiply-strings/description/)

Given two non-negative integers num1 and num2 represented as strings, return the product of num1 and num2.

**Note:** 

1. The length of both num1 and num2 is &lt; 110.
2. Both num1 and num2 contains only digits 0-9.
3. Both num1 and num2 does not contain any leading zero.
4. You must not use any built-in BigInteger library or convert the inputs to integer directly.

**Example:**

```text

```

## Thought Process {#thought-process}

1. Multiply from Back
   1. Start the multiplication from the back, each time we will have at most 2 digits
   2. We need 

## Solution

```java
class Solution {
    public String multiply(String num1, String num2) {
        if (num1.equals("0") || num2.equals("0")) return "0";
        int m = num1.length(), n = num2.length();
        int[] pos = new int[m + n];
        char[] n1 = num1.toCharArray(), n2 = num2.toCharArray();
        for (int i = m - 1; i >= 0; i--){
            for (int j = n - 1; j >= 0; j--){
                int mul = (n1[i] - '0') * (n2[j] - '0');
                int p1 = i + j, p2 = i + j + 1;
                int sum = mul + pos[p2];
                pos[p1] += sum /10;
                pos[p2] = sum % 10;
            }
        }
        StringBuilder sb = new StringBuilder();
        int i = 0;
        while (pos[i] == 0) i++;
        while (i < pos.length) sb.append(pos[i++]);
        return sb.toString();
    }
}
```

## Additional {#additional}


# 067-add-binary

## Question {#question}

[https://leetcode.com/problems/add-binary/description/](https://leetcode.com/problems/add-binary/description/)

Given two binary strings, return their sum \(also a binary string\).

**Example:**

```text
a = "11"
b = "1"
Return "100".
```

## Thought Process {#thought-process}

1. Scan Backward
   1. At the number from the back
   2. When the character is the same, we simply append the carry and update the carry accordingly
   3. When the character is different, we append the opposite of the carry
   4. At the end, we reverse the string builder

## Solution

```java
class Solution {
    public String addBinary(String a, String b) {
        int m = a.length() - 1, n = b.length() - 1;
        StringBuilder sb = new StringBuilder();
        char prev = '0';
        while(m >= 0 || n >= 0){
            char c1 = m < 0 ? '0' : a.charAt(m);
            char c2 = n < 0 ? '0' :b.charAt(n);
            if(c1 == c2){
                sb.append(prev);
                prev = c1;
            } else if (prev == '1'){
                sb.append('0');
            } else{
                sb.append('1');
            }
            m--;
            n--;
        }
        if(prev == '1') sb.append('1');
        return sb.reverse().toString();
    }
}
```

## Additional {#additional}


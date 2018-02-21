### Question {#question}

[https://leetcode.com/problems/fraction-to-recurring-decimal/description/](https://leetcode.com/problems/fraction-to-recurring-decimal/description/)

Given two integers representing the numerator and denominator of a fraction, return the fraction in string format.

If the fractional part is repeating, enclose the repeating part in parentheses.

**Example:**

```
Given numerator = 1, denominator = 2, return "0.5".
Given numerator = 2, denominator = 1, return "2".
Given numerator = 2, denominator = 3, return "0.(6)".
```

### Thought Process {#thought-process}

1. StringBuilder and Map
   1. Follow the rule of division, save the output to the string builder
   2. The repeating part happens when we have visited the remainder before, then we need to insert the "\(" at the position provided by the map
   3. Time com

### Solution

```java
class Solution {
    public String fractionToDecimal(int numerator, int denominator) {
        if (numerator == 0) return "0";
        String sign = (numerator > 0) ^ (denominator > 0) ? "-" : "";
        long num = Math.abs((long) numerator);
        long den = Math.abs((long) denominator);
        StringBuilder sb = new StringBuilder();
        sb.append(sign).append(num / den);
        num %= den;
        if (num == 0) return sb.toString();
        sb.append(".");
        Map<Long, Integer> map = new HashMap<>();
        int index = sb.length();
        while (num != 0) {
            if (map.containsKey(num)) {
                sb.insert(map.get(num), "(");
                sb.append(")");
                break;
            }
            map.put(num, index++);
            num *= 10;
            sb.append(num / den);
            num %= den;
        }
        return sb.toString();
    }
}
```

### Additional {#additional}




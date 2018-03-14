### Question {#question}

[https://leetcode.com/problems/basic-calculator/description/](https://leetcode.com/problems/basic-calculator/description/)

Implement a basic calculator to evaluate a simple expression string.

The expression string may contain open \( and closing parentheses \), the plus + or minus sign -, non-negative integers and empty spaces .

You may assume that the given expression is always valid.

**Example:**

```
"1 + 1" = 2
" 2-1 + 2 " = 3
"(1+(4+5+2)-3)+(6+8)" = 23
```

### Thought Process {#thought-process}

1. Stack
   1. Use variable to keep track of the number, using num = num \* 10 + curVal
   2. When we see a operator, + and -, its time to evaluate previous expression, update the sign and reset num
   3. We also need another variable, sign, to simply the formula
   4. Time complexity O\(n\)
   5. Space complexity O\(n\)

### Solution

```java
class Solution {
    public int calculate(String s) {
        char[] chars = s.toCharArray();
        int result = 0, sign = 1, num = 0;
        Stack<Integer> stack = new Stack<>();
        stack.push(sign);
        for (int i = 0; i < chars.length; i++) {
            if (chars[i] >= '0' && chars[i] <= '9') {
                num = num * 10 + chars[i] - '0';
            } else if (chars[i] == '+' || chars[i] == '-') {
                result += sign * num;
                sign = stack.peek() * (chars[i] == '+' ? 1 : -1);
                num = 0;
            } else if (chars[i] == '(') {
                stack.push(sign);
            } else if (chars[i] == ')') {
                stack.pop();
            }
        }
        result += sign * num;
        return result;
    }
}
```

### Additional {#additional}




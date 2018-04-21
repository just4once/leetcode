### Question {#question}

[https://leetcode.com/problems/basic-calculator-ii/description/](https://leetcode.com/problems/basic-calculator-ii/description/)

Implement a basic calculator to evaluate a simple expression string.

The expression string contains only non-negative integers, +, -, \*, / operators and empty spaces . The integer division should truncate toward zero.

You may assume that the given expression is always valid.

**Example:**

```
"3+2*2" = 7
" 3/2 " = 1
" 3+5 / 2 " = 5
```

### Thought Process {#thought-process}

1. Switch at Different Character
   1. When the character is ' ', we skip
   2. We break the expression into different chunks by '+' and '-', because we know it's time to finishing the evaluation. When we encounter '\*' and '/' we need to keep saving the result to a product variable
   3. When the character is either '+' or '-', we need to finish the previous operation whether it was division or multiplication, sign \* product / num or sign \* product \* num and add it to the result.

```java
class Solution {
    public int calculate(String s) {
        int result = 0, num = 0;
        int sign = 1, product = 1;
        boolean wasDivide = false;
        for (char c : s.toCharArray()) {
            if (c == ' ') continue;
            switch (c) {
                case '+':
                case '-':
                    result += wasDivide ? sign * product / num : sign * product * num;
                    num = 0;
                    product = 1;
                    sign = c == '+' ? 1 : -1;
                    wasDivide = false;
                    break;
                case '*':
                case '/':
                    product = wasDivide ? product / num : product * num;
                    num = 0;
                    wasDivide = c == '/';
                    break;
                default:
                    num = num * 10 + c - '0';
            }
            
        }
        result += wasDivide ? sign * product / num : sign * product * num;
        return result;
    }
}
```

### Additional {#additional}




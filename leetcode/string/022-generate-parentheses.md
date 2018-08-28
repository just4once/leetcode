# 022-generate-parentheses

## Question {#question}

[https://leetcode.com/problems/generate-parentheses/description/](https://leetcode.com/problems/generate-parentheses/description/)

Givennpairs of parentheses, write a function to generate all combinations of well-formed parentheses.

For example, givenn= 3, a solution set is:

**Example:**

```text
[
  "((()))",
  "(()())",
  "(())()",
  "()(())",
  "()()()"
]
```

## Thought Process {#thought-process}

1. Backtrack
   1. Use two variable to keep track left bracket and right bracket, open and close
   2. Increase the count until we open + close == 2 \* n
   3. As long we have more room to add left, we add left bracket first
   4. And then we add right bracket when right bracket usage is less than the left
   5. Time complexity O\(4^n/sqrt\(n\)\)
   6. Space complexity O\(4^n/sqrt\(n\)\)

## Solution

```java
class Solution {
    public List<String> generateParenthesis(int n) {
        List<String> result = new ArrayList<>();
        char[] chars = new char[n * 2];
        backtrack(result, chars, 0, 0);
        return result;
    }

    public void backtrack(List<String> result, char[] chars, int open, int close) {
        if (open + close == chars.length) {
            result.add(new String(chars));
            return;
        }
        if (open < chars.length / 2) {
            chars[open + close] = '(';
            backtrack(result, chars, open + 1, close);
        }
        if (close < open) {
            chars[open + close] = ')';
            backtrack(result, chars, open, close + 1);
        }
    }
}
```

## Additional {#additional}


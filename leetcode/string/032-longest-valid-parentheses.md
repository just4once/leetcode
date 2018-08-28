# 032-longest-valid-parentheses

## Question {#question}

[https://leetcode.com/problems/longest-valid-parentheses/description/](https://leetcode.com/problems/longest-valid-parentheses/description/)

Given a string containing just the characters '\(' and '\)', find the length of the longest valid \(well-formed\) parentheses substring.

**Example:**

```text
For "(()", the longest valid parentheses substring is "()", which has length = 2.
Another example is ")()())", where the longest valid parentheses substring is "()()", which has length = 4.
```

## Thought Process {#thought-process}

1. Dynamic Programing
   1. A valid string always ends with \), so we check when we encounter \)
   2. When current character is \) and last character is \(, we increase by 2, dp\[i\] = dp\[i - 2\] + 2
   3. When the last character is \) and last character is \) we need to investigate chars\[i - dp\[ i - 1\] - 1\] is equal to \(, if that's the case, we can increase the count by 2 in addition to dp\[i - 1\] and also any valid string before i - dp\[i - 1\] - 1, or simply dp\[i - dp\[i - 1\] - 2, so dp\[i\] = dp\[i - 1\] + dp\[i - dp\[i - 1\] - 2\] + 2
   4. Time complexity O\(n\)
   5. Space complexity O\(n\)
2. Stack
   1. Use stack to save the index 
3. asd

## Solution

```java
class Solution {
    public int longestValidParentheses(String s) {
        if (s == null) return 0;
        int[] dp = new int[s.length() + 1];
        s = 'x' + s;
        int max = 0;
        char[] chars = s.toCharArray();
        for (int i = 2; i < chars.length; i++) {
            if (chars[i] == ')') {
                if (chars[i - 1] == '(') {
                    dp[i] = dp[i - 2] + 2;
                } else if (chars[i - dp[i - 1] - 1] == '(') {
                    dp[i] = dp[i - 1] + dp[i - dp[i - 1] - 2] + 2;
                }
                max = Math.max(max, dp[i]);
            }
        }
        return max;
    }
}
```

```java
class Solution {
    public int longestValidParentheses(String s) {
        if (s == null) return 0;
        Stack<Integer> stack = new Stack<>();
        stack.push(-1); // the index of the start - 1
        int len = 0;
        for (int i = 0; i < s.length(); i++) {
            if (s.charAt(i) == '(') {
                stack.push(i);
            } else {
                stack.pop();
                if (stack.isEmpty()) stack.push(i);
                len = Math.max(len, i - stack.peek());
            }
        }
        return len;
    }
}
```

```java
public class Solution {
    public int longestValidParentheses(String s) {
        int left = 0, right = 0, max = 0;
        for (int i = 0; i < s.length(); i++) {
            if (s.charAt(i) == '(') left++;
            else right++;
            if (left == right) max = Math.max(max, 2 * right);
            else if (right > left) left = right = 0;
        }
        left = right = 0;
        for (int i = s.length() - 1; i >= 0; i--) {
            if (s.charAt(i) == ')') right++;
            else left++;
            if (left == right) max = Math.max(max, 2 * left);
            else if (left > right) left = right = 0;
        }
        return max;
    }
}
```

## Additional {#additional}


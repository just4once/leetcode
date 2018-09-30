# 282-expression-add-operators

## Question {#question}

Given a string that contains only digits `0-9` and a target value, return all possibilities to add **binary** operators \(not unary\) `+`, `-`, or `*`between the digits so they evaluate to the target value.

**Example 1:**

```text
Input: num = "123", target = 6
Output: ["1+2+3", "1*2*3"] 
```

**Example 2:**

```text
Input: num = "232", target = 8
Output: ["2*3+2", "2+3*2"]
```

**Example 3:**

```text
Input: num = "105", target = 5
Output: ["1*0+5","10-5"]
```

**Example 4:**

```text
Input: num = "00", target = 0
Output: ["0+0", "0-0", "0*0"]
```

**Example 5:**

```text
Input: num = "3456237490", target = 9191
Output: []
```



## Thought Process {#thought-process}

1. Divide and Conquer
   1. We can divide the number at each position and check if there is way to get target using different operations
   2. At each position \(after getting the value\), we recursively look at these three operations
   3. If we only have +-, the computation is easier, we can move forward without worry about the previous value being used in multiply
   4. Now, we need a separate variable to hold the previous value and reverse the result by subtracting previous value and then compute with right order
   5. We create a separate function recur\(chars, index, value,  pre, stringbuilder, target, result\) where index points to the current character and value is the current evaluated result, pre is previous number, stringbuilder holds the 
   6. Time complexity O\(n\*3^n\), where n^2 comes from n loops and n character in stringBuilder.toString\(\), and 3^n from 3 operators and looping for each digit
   7. Space complexity O\(n^2\*3^n\), where n^2 comes from ways to break operands
   8. Other suggests:
   9. T\(n\) = 3  _T\(n-1\) + 3_  T\(n-2\) + 3  _T\(n-3\) + ... + 3_ T\(1\); 
   10. T\(n-1\) = 3  _T\(n-2\) + 3_  T\(n-3\) + ... 3 \* T\(1\); 
   11. Thus T\(n\) = 4T\(n-1\);
2. Divide and Conquer \(with path array\)
   1. Instead of using string builder, we use a char array to save the path that get to the current point, if the value == target, we can save the path
   2. Moreover, we can also postpone the operation until we meet the next operator, this way we don't have to do any retracting

## Solution

```java
class Solution {
    public List<String> addOperators(String num, int target) {
        // If the question is simply +-, the result is easy
        // because we have *, we need to track previous number and
        // reverse when we use multiply
        List<String> res = new ArrayList<>();
        if (num.length() == 0) return res;
        char[] chars = num.toCharArray();
        long value = 0;
        StringBuilder sb = new StringBuilder();
        for (int i = 0; i < chars.length; i++) {
            // try each reak point
            value = value * 10 + chars[i] - '0';
            sb.setLength(0);
            sb.append(value);
            recur(chars, i + 1, value, value, sb, target, res);
            if (chars[0] == '0') break;
        }
        return res;
    }
    
    private void recur(char[] chars, int index, long value, long pre, StringBuilder sb, int target, List<String> res) {
        if (index == chars.length) {
            if (value == target) res.add(sb.toString());
        } else {
            // initialize
            long cur = 0;
            // save the length for backtrack
            int len = sb.length();
            for (int i = index; i < chars.length; i++) {
                cur = cur * 10 + chars[i] - '0';
                // multiply
                recur(chars, i + 1, value - pre + pre * cur, pre * cur, sb.append("*").append(cur), target, res);
                sb.setLength(len);
                // add
                recur(chars, i + 1, value + cur, cur, sb.append("+").append(cur), target, res);
                sb.setLength(len);
                // subtract
                recur(chars, i + 1, value - cur, -cur, sb.append("-").append(cur), target, res);
                sb.setLength(len);
                if (chars[index] == '0') break;
            }
        }
    }
}
```

```java
class Solution {
    public List<String> addOperators(String num, int target) {
        // If the question is simply +-, the result is easy
        // because we have *, we need to track previous number and
        // reverse when we use multiply
        List<String> res = new ArrayList<>();
        if (num.length() == 0) return res;
        char[] chars = num.toCharArray();
        int n = chars.length;
        char[] path = new char[2 * n - 1];
        long value = 0;
        for (int i = 0; i < chars.length; i++) {
            // try each reak point
            value = value * 10 + chars[i] - '0';
            path[i] = chars[i];
            recur(chars, i + 1, 0, value, path, i + 1, target, res);
            if (value == 0) break;
        }
        return res;
    }
    
    private void recur(char[] chars, int index, long left, long pre, char[] path, int len, int target, List<String> res) {
        if (index == chars.length) {
            if (left + pre == target) res.add(new String(path, 0, len));
        } else {
            // initialize
            long cur = 0;
            int j = len + 1;
            for (int i = index; i < chars.length; i++) {
                cur = cur * 10 + chars[i] - '0';
                path[j++] = chars[i];
                // multiply
                path[len] = '*';
                recur(chars, i + 1, left, pre * cur, path, j, target, res);
                // add
                path[len] = '+';
                recur(chars, i + 1, left + pre, cur, path, j, target, res);
                // subtract
                path[len] = '-';
                recur(chars, i + 1, left + pre, -cur, path, j, target, res);
            }
        }
    }
}
```

## Additional {#additional}


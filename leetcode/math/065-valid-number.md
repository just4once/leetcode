### Question {#question}

[https://leetcode.com/problems/valid-number/description/](https://leetcode.com/problems/valid-number/description/)

Validate if a given string is numeric.

**Example:**

```
"0" => true
" 0.1 " => true
"abc" => false
"1 a" => false
"2e10" => true
```

Note: It is intended for the problem statement to be ambiguous. You should gather all requirements up front before implementing one.

### Thought Process {#thought-process}

1. Trim
   1. We first trim the leading spaces and trailing spaces
   2. For each character we visit we decide its validity
   3. The boolean variable leftSeen and rightSeen track the validity of the number as whole, even when the number is an integer
   4. For the integer, we can just assign these two variables to true after getting a number
   5. For the double, we need to have number on at least one side
   6. For the scientific notation, we need to make sure we get a number before the notation
   7. The pointSeen and eSeen boolean variable help to track the difference in type of number we are dealing with
   8. Time complexity O\(n\)
   9. Space complexity O\(1\)

### Solution

```java
class Solution {
    public boolean isNumber(String s) {
        if (s == null) return false;
        s = s.trim();
        boolean leftSeen = false, rightSeen = false;
        boolean pointSeen = false, eSeen = false;
        for (int i = 0; i < s.length(); i++) {
            char c = s.charAt(i);
            if (Character.isDigit(c)) {
                leftSeen = true;
                rightSeen = true;
            } else if (c == '.') {
                if (pointSeen || eSeen) return false;
                pointSeen = true;
            } else if (c == 'e') {
                if (!leftSeen || eSeen) return false;
                eSeen = true;
                rightSeen = false;
            } else if (c == '+' || c == '-') {
                if (i != 0 && s.charAt(i - 1) != 'e') return false;
            } else {
                return false;
            }
        }
        return leftSeen && rightSeen;
    }
}
```

### Additional {#additional}




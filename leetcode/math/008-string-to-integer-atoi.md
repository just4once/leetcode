### Question {#question}

[https://leetcode.com/problems/string-to-integer-atoi/description/](https://leetcode.com/problems/string-to-integer-atoi/description/)

Implement`atoi`to convert a string to an integer.

**Hint: **Carefully consider all possible input cases. If you want a challenge, please do not see below and ask yourself what are the possible input cases.

**Notes: **It is intended for this problem to be specified vaguely \(ie, no given input specs\). You are responsible to gather all the input requirements up front.

**Requirements for atoi:**

The function first discards as many whitespace characters as necessary until the first non-whitespace character is found. Then, starting from this character, takes an optional initial plus or minus sign followed by as many numerical digits as possible, and interprets them as a numerical value.

The string can contain additional characters after those that form the integral number, which are ignored and have no effect on the behavior of this function.

If the first sequence of non-whitespace characters in str is not a valid integral number, or if no such sequence exists because either str is empty or it contains only whitespace characters, no conversion is performed.

If no valid conversion could be performed, a zero value is returned. If the correct value is out of the range of representable values, INT\_MAX \(2147483647\) or INT\_MIN \(-2147483648\) is returned.

**Example:**

```

```

### Thought Process {#thought-process}

1. Check Character
   1. Move the pointer to the first non-space character
   2. Check the sign
   3. Check the current character is valid digit
   4. Check the result is within the boundary of interger
   5. Time complexity O\(n\)
   6. Space complexity O\(1\)

### Solution

```java
class Solution {
    public int myAtoi(String str) {
        if (str == null || str.length() == 0) return 0;
        int i = 0, res = 0, sign = 1;
    char[] chars = str.toCharArray();
    while (i < chars.length && chars[i] == ' ')
        i++;

    if (i < chars.length && isSign(chars[i])) {
        sign = chars[i] == '-' ? -1 : 1;
        i++;
    }
    while (i < chars.length) {
        int digit = chars[i] - '0';
        if (!isValidDigit(digit)) break;
        if (isOutOfBoundary(res, digit)) return sign == 1 ? Integer.MAX_VALUE : Integer.MIN_VALUE;
        res = res * 10 + digit;
        i++;
    }
    return sign * res;
    }

    public boolean isSign(char c){
        return c == '-' || c == '+';
    }

    public boolean isValidDigit(int i) {
        return i >= 0 && i < 10;
    }

    public boolean isOutOfBoundary(int i, int tail){
        return i > Integer.MAX_VALUE / 10 || (i == Integer.MAX_VALUE / 10 && tail > Integer.MAX_VALUE % 10);
    }
}
```

### Additional {#additional}




### Question {#question}

[https://leetcode.com/problems/reverse-integer/description/](https://leetcode.com/problems/reverse-integer/description/)

Given a 32-bit signed integer, reverse digits of an integer.

**Example:**

```
Input: 123
Output:  321

Input: -123
Output: -321

Input: 120
Output: 21
```

### Thought Process {#thought-process}

1. Reverse digit by digit
   1. Check for potential overflow as we obtain the result
   2. Time complexity O\(d\), where d is number of digits
   3. Space complexity O\(1\)

### Solution

```java
class Solution {
    public int reverse(int x) {
        long res = 0;
        while(x != 0){
            res = res * 10 + x % 10;
            if (res > Integer.MAX_VALUE || res < Integer.MIN_VALUE) return 0;
            x /= 10;
        }
        return (int) res;
    }
}
```

```java
class Solution {
    public int reverse(int x) {
        int res = 0;
        while(x != 0){
            int tmp = res * 10 + x % 10;
            if (tmp / 10 != res) return 0;
            res = tmp;
            x /= 10;
        }
        return res;
    }
}
```

### Additional {#additional}




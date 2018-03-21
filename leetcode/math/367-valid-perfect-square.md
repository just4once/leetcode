### Question {#question}

[https://leetcode.com/problems/valid-perfect-square/description/](https://leetcode.com/problems/valid-perfect-square/description/)

Given a positive integer num, write a function which returns True if num is a perfect square else False.

**Example:**

```
Input: 16
Returns: True

Input: 14
Returns: False
```

### Thought Process {#thought-process}

1. Binary Search
   1. We choose the mid and adjust low and high accordingly
   2. Time complexity O\(log n\)
   3. Space complexity O\(1\)
2. Newton's Method
   1. We can refer to [Newton Method](https://en.wikipedia.org/wiki/Integer_square_root#Using_only_integer_division), where we want to solve x^2 - n = 0
   2. $$x_1 = x_0 - f(x_0)/f'(x_0)$$
   3. $$x_1 = (x_0 + n / x_0) / 2$$
   4. Time complexity O\(log n\)
   5. Space complexity O\(1\)

### Solution

```java
class Solution {
    public boolean isPerfectSquare(int num) {
        long lo = 1, hi = num;
        while (lo <= hi) {
            long mi = lo + (hi - lo) / 2;
            if (mi * mi == num) return true;
            else if (mi * mi < num) lo = mi + 1;
            else hi = mi - 1;
        }
        return false;
    }
}
```

```java
class Solution {
    public boolean isPerfectSquare(int num) {
        long x = num;
        while (x * x > num) {
            x = (x + num / x) / 2;
        }
        return x * x == num;
    }
}
```

### Additional {#additional}




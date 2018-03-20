### Question {#question}

[https://leetcode.com/problems/count-numbers-with-unique-digits/description/](https://leetcode.com/problems/count-numbers-with-unique-digits/description/)

Given a non-negative integer n, count all numbers with unique digits, x, where 0 ≤ x &lt; 10^n.

**Example:**

```
Given n = 2, return 91. 
(The answer should be the total numbers in the range of 0 ≤ x < 100, 
excluding [11,22,33,44,55,66,77,88,99])
```

### Thought Process {#thought-process}

1. DP
   1. Start from n = 1, we have 10 choices
   2. For n = 2, we can only have 9 choice for the first digit \(excluding 0\), and 9 choices for the second digit \(avoiding the same number\), 9 \* 9 unique 2 digits number in additional to the 10 before
   3. For n = 3, we have 9, 9, and 8 choice for each digit, 9 \*9 \* 8 in additional to 91 before
   4. Time complexity O\(n\) or O\(10\) at most
   5. Space complexity O\(1\)

### Solution

```java
class Solution {
    public int countNumbersWithUniqueDigits(int n) {
        int res = 1;
        int choice = 9, available = 9;
        while (n-- >= 1 && available > 0) {
            res += choice;
            choice *= available;
            available--;
        }
        return res;
    }
}
```

### Additional {#additional}




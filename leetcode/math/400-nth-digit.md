# 400-nth-digit

## Question {#question}

[https://leetcode.com/problems/nth-digit/description/](https://leetcode.com/problems/nth-digit/description/)

Find the nth digit of the infinite integer sequence 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, ...

**Example:**

```text
Input:
3

Output:
3
```

```text
Input:
11

Output:
0

Explanation:
The 11th digit of the sequence 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, ... is a 0, which is part of the number 10.
```

## Thought Process {#thought-process}

1. Math
   1. The problem can be break down into different group based on the digits, 1 - 9, 10 - 99, where the count is 9, 90, and etc
   2. Time complexity O\(log n\)
   3. Space complexity O\(1\)

## Solution

```java
class Solution {
    public int findNthDigit(int n) {
        int len = 1;
        long count = 9;
        int start = 1;
        while (n > len * count) {
            n -= len * count;
            count *= 10;
            start *= 10;
            len++;
        }
        start += (n - 1) / len;
        return Integer.toString(start).charAt((n - 1) % len) - '0';
    }
}
```

## Additional {#additional}


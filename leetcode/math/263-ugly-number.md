# 263-ugly-number

## Question {#question}

[https://leetcode.com/problems/ugly-number/description/](https://leetcode.com/problems/ugly-number/description/)

Write a program to check whether a given number is an ugly number.

Ugly numbers are positive numbers whose prime factors only include 2, 3, 5. For example, 6, 8 are ugly while 14 is not ugly since it includes another prime factor 7.

Note that 1 is typically treated as an ugly number.

**Example:**

```text

```

## Thought Process {#thought-process}

1. Divide All Factors
   1. While we can divide an factor perfectly, we divide
   2. At the end, we compare the final num to 1

## Solution

```java
class Solution {
    public boolean isUgly(int num) {
        if (num <= 0) return false;
        while (num % 2 == 0) num /= 2;
        while (num % 3 == 0) num /= 3;
        while (num % 5 == 0) num /= 5;
        return num == 1;
    }
}
```

## Additional {#additional}


# 258-add-digits

## Question {#question}

[https://leetcode.com/problems/add-digits/description/](https://leetcode.com/problems/add-digits/description/)

Given a non-negative integer num, repeatedly add all its digits until the result has only one digit.

**Example:**

```text
Given num = 38, the process is like: 3 + 8 = 11, 1 + 1 = 2. Since 2 has only one digit, return it.
```

## Thought Process {#thought-process}

1. Loop
   1. While the num &gt; 9, we compute
   2. The computation simply add all the digt
   3. Time complexity O\(d\)
   4. Space complexity O\(1\)
2. Find pattern
   1. If you observe the cycle repeats from 1 to 9 for range of 9, such as 1 to 9, 10 - 18, 19 to 27, and etc
   2. Time complexity 

## Solution

```java
class Solution {
    public int addDigits(int num) {
        int tmp;
        while (num > 9) {
            tmp = 0;
            while (num > 0) {
                tmp += num % 10;
                num /= 10;
            }
            num = tmp;
        }
        return num;
    }
}
```

```java
class Solution {
    public int addDigits(int num) {
        return 1 + (num - 1) % 9;
    }
}
```

## Additional {#additional}


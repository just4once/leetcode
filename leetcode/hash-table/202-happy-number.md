# 202-happy-number

## Question {#question}

[https://leetcode.com/problems/happy-number/description/](https://leetcode.com/problems/happy-number/description/)

Write an algorithm to determine if a number is "happy".

A happy number is a number defined by the following process: Starting with any positive integer, replace the number by the sum of the squares of its digits, and repeat the process until the number equals 1 \(where it will stay\), or it loops endlessly in a cycle which does not include 1. Those numbers for which this process ends in 1 are happy numbers.

**Example:**

```text
19 is a happy number

1^2 + 9^2 = 82
8^2 + 2^2 = 68
6^2 + 8^2 = 100
1^2 + 0^2 + 0^2 = 1
```

## Thought Process {#thought-process}

1. Brute Force - Set
   1. Use set to record the squared sum through the process
   2. If we have seen this number before, we know there is loop, and we cannot reach to 1
2. asd

## Solution

```java
class Solution {
    public boolean isHappy(int n) {
        Set<Integer> set = new HashSet<>();
        int res = 0;
        while (set.add(n)) {
            if (n == 1) return true;
            while (n > 0) {
                int d = n % 10;
                res += d * d;
                n /= 10;
            }
            n = res;
            res = 0;
        }
        return false;
    }
}
```

```java
class Solution {
    public boolean isHappy(int n) {
        int slow = n, fast = n;
        do {
            slow = cal(slow);
            fast = cal(cal(fast));
        } while (slow != fast);
        return slow == 1;
    }

    private int cal(int n) {
        int res = 0;
        while (n > 0) {
            int d = n % 10;
            res += d * d;
            n /= 10;
        }
        return res;
    }
}
```

## Additional {#additional}


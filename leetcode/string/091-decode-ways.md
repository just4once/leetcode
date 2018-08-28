# 091-decode-ways

## Question {#question}

[https://leetcode.com/problems/decode-ways/description/](https://leetcode.com/problems/decode-ways/description/)

A message containing letters from A-Z is being encoded to numbers using the following mapping:

```text
'A' -> 1
'B' -> 2
...
'Z' -> 26
```

Given an encoded message containing digits, determine the total number of ways to decode it.

```text
Given encoded message "12", it could be decoded as "AB" (1 2) or "L" (12).
The number of ways decoding "12" is 2.
```

## Thought Process {#thought-process}

1. Dynamic Programing
   1. For every character we are exploring, we need to check it along with previous character
   2. We create an array of dp\[n + 1\] to store the number ways of deciphering, and dp\[i\] store the result for ith character
   3. if the character is 0, it has to be use in conjunction with previous character
   4. If the character is non 0, it has to be at least as dp\[i - 1\]
   5. if the character combine with previous character is between 10 and 26 inclusive, we need to add dp\[i - 2\]
   6. Time complexity O\(n\)
   7. Space complexity O\(n\)
2. Dynamic Programing - Space Reduction
   1. If we observe closely, we can see that the dp only depends on i - 1 and i - 2, so we just need two variables
   2. pre1 and pre2
   3. Time complexity O\(n\)
   4. Space complexity O\(1\)

## Solution

```java
class Solution {
    public int numDecodings(String s) {
        if (s == null || s.length() == 0 || s.charAt(0) == '0') return 0;
        char[] chars = s.toCharArray();
        int n = chars.length;
        // dp[i] store the ith character
        int[] dp = new int[n + 1];
        dp[0] = 1;
        dp[1] = 1;
        for (int i = 2; i < dp.length; i++) {
            int cur = chars[i - 1] - '0';
            int pre = (chars[i - 2] - '0' ) * 10 + cur;
            if (cur != 0) dp[i] = dp[i - 1];
            if (pre >= 10 && pre <= 26) dp[i] += dp[i - 2];
        }
        return dp[n];
    }
}
```

## Additional {#additional}


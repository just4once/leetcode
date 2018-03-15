### Question {#question}

[https://leetcode.com/problems/perfect-squares/description/](https://leetcode.com/problems/perfect-squares/description/)

Given a positive integer n, find the least number of perfect square numbers \(for example, 1, 4, 9, 16, ...\) which sum to n.

**Example:**

```
Given n = 12, return 3 because 12 = 4 + 4 + 4; given n = 13, return 2 because 13 = 4 + 9.
```

### Thought Process {#thought-process}

1. DP
   1. Use array of n + 1 to store the count
   2. Every time the, we try to see the best solution by checking all the i - j \* j count, where i is the current element and j range to 1 until sqrt\(i\)
   3. Time complexity O\(n^1.5\)
   4. Space complexity O\(n\)
2. Math
   1. Base on [Lagrange's four-square theorem](https://en.wikipedia.org/wiki/Lagrange%27s_four-square_theorem), the answer is limit by 4
   2. 

### Solution

```java
class Solution {
    public int numSquares(int n) {
        int[] dp = new int[n + 1];
        for (int i = 1; i <= n; i++) {
            dp[i] = i;
            for (int j = 1; j * j <= i; j++) {
                dp[i] = Math.min(dp[i], dp[i - j * j] + 1);
            }
        }
        return dp[n];
    }
}
```

```java

```

### Additional {#additional}




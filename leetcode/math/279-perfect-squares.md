# 279-perfect-squares

## Question {#question}

[https://leetcode.com/problems/perfect-squares/description/](https://leetcode.com/problems/perfect-squares/description/)

Given a positive integer n, find the least number of perfect square numbers \(for example, 1, 4, 9, 16, ...\) which sum to n.

**Example:**

```text
Given n = 12, return 3 because 12 = 4 + 4 + 4; given n = 13, return 2 because 13 = 4 + 9.
```

## Thought Process {#thought-process}

1. DP
   1. Use array of n + 1 to store the count
   2. Every time the, we try to see the best solution by checking all the i - j \* j count, where i is the current element and j range to 1 until sqrt\(i\)
   3. Time complexity O\(n^1.5\)
   4. Space complexity O\(n\)
2. Math
   1. Base on \[Lagrange's four-square theorem\]\(\[[https://en.wikipedia.org/wiki/Lagrange's\_four-square\_theorem\]\(https://en.wikipedia.org/wiki/Lagrange's\_four-square\_theorem\)\](https://en.wikipedia.org/wiki/Lagrange's_four-square_theorem]%28https://en.wikipedia.org/wiki/Lagrange's_four-square_theorem%29\)\), the answer is limit by 4
   2. The number representation can be found here, [http://www.alpertron.com.ar/4SQUARES.HTM](http://www.alpertron.com.ar/4SQUARES.HTM)
   3. Perfect squares has one factor
   4. If the representation is 4^k\*\(8\*m + 7\), there are 4 factors
   5. If the n - perfectSquare is also a perfect square, then there are two factors
   6. Otherwise there are 3 factors
   7. Time complexity O\(1\)
   8. Space complexity O1\)

## Solution

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
class Solution {
    public int numSquares(int n) {
        if (isPerfectSquare(n)) return 1;
        while (n % 4 == 0) n /= 4;
        if (n % 8 == 7) return 4;
        for (int i = 1; i * i <= n; i++) {
            if (isPerfectSquare(n - i * i)) return 2;
        }
        return 3;
    }

    private boolean isPerfectSquare(int i) {
        int a = (int) Math.sqrt(i);
        return a * a == i;
    }
}
```

## Additional {#additional}


# 887-super-egg-drop

## Question {#question}

[https://leetcode.com/problems/super-egg-drop/description/](https://leetcode.com/problems/super-egg-drop/description/)

You are given `K` eggs, and you have access to a building with `N` floors from `1` to `N`. 

Each egg is identical in function, and if an egg breaks, you cannot drop it again.

You know that there exists a floor `F` with `0 <= F <= N` such that any egg dropped at a floor higher than `F` will break, and any egg dropped at or below floor `F` will not break.

Each _move_, you may take an egg \(if you have an unbroken one\) and drop it from any floor `X` \(with `1 <= X <= N`\). 

Your goal is to know **with certainty** what the value of `F` is.

What is the minimum number of moves that you need to know with certainty what `F` is, regardless of the initial value of `F`?

**Example 1:**

```text
Input: K = 1, N = 2
Output: 2
Explanation: 
Drop the egg from floor 1.  If it breaks, we know with certainty that F = 0.
Otherwise, drop the egg from floor 2.  If it breaks, we know with certainty that F = 1.
If it didn't break, then we know with certainty F = 2.
Hence, we needed 2 moves in the worst case to know what F is with certainty.
```

**Example 2:**

```text
Input: K = 2, N = 6
Output: 3
```

**Example 3:**

```text
Input: K = 3, N = 14
Output: 4
```

**Note:**

1. `1 <= K <= 100`
2. `1 <= N <= 10000`

## Thought Process {#thought-process}

1. Brute Force with DP \(TLE\)
   1. We create an dp array to store the best moves for each eggs and floors combination, where dp\[i\]\[j\] represents the moves for i eggs and j floors
   2. For current eggs and floors, the best moves is obtained by dropping the egg from 1st floor up to current floor
   3. The minimum of all these drop tests are our answer
   4. For each test on ith floor, ranges from 1 to current floor, the egg could either break, so we need to use less egg on remaining floor dp\[curEgg - 1\]\[i - 1\], or it doesn't, so we use dp\[curEgg\]\[curFloor - i\]
   5. Because we are expecting worst case, the maximum of them + 1 \(current egg drop\) is the answer for dropping at ith floor
   6. Time complexity O\(KN^2\)
   7. Space complexity O\(KN\)
2. DP with Binary
   1. Notice the function dp\( K - 1, i - 1\) increases when i increase, while on the other hand, dp\(K, N - i\) decreases when i increase
   2. We can use this observation to speed up the search for minimum i
   3. Time complexity O\(KNlogN\)
   4. Space complexity O\(KN\)
3. DP with Optimality
   1. Looking at second function, the value increase when N increase, where the i\_opt \(current optimal\) can be use as the starting point for next N
   2. Time complexity O\(KN\)
   3. Space complexity O\(KN\)
4. DP with Problem Rephrase
   1. Instead of asking how many moves, we rephrase the question into how many floor we can cover for m moves, and K egg
   2. We create dp array, where dp\[m\]\[k\] stores the floors that we can cover using m moves and k eggs
   3. For a floor X, when we drop the egg, there are two cases happen here
   4. If the egg breaks, we need to go down to check dp\[m - 1\]\[k - 1\], we cover dp\[m - 1\]\[k - 1\] + 1 + Y \(top of X\) floors
   5. Else If the egg doesn't break, we go up and check dp\[m - 1\]\[k\], we cover X + dp\[m -1\]\[k\] floors
   6. Where we can summarize into dp\[m\]\[k\] = dp\[m - 1\]\[k - 1\] + dp\[m - 1\]\[k\] + 1
   7. Time complexity O\(KlogN\)
   8. Space complexity O\(KN\)
5. DP above - 1D
   1. We can reduce the space to O\(k\)
   2. Since dp\[m\]\[k\] depends on the last row only, we can use dp\[K+1\] to store all the information
   3. Instead going from forward, we need to travel from backward in order to avoid using the updated value
   4. Time complexity O\(KlogN\)
   5. Space complexity O\(K\)

## Solution

```java
class Solution {
    public int superEggDrop(int K, int N) {
        int[][] memo = new int[K + 1][N + 1];
        // define memo[i][j] to be the number of moves for i eggs and j floors
        return dp(memo, K, N);
    }
    
    private int dp(int[][] memo, int K, int N) {
        if (N <= 1) return 1;
        if (K == 1) return N;
        if (memo[K][N] > 0) return memo[K][N];
        // now for current K and N, the problem can break down into dropping eggs
        // from i = [1, N] floors.
        // For each floor, the egg either breaks so we use less egg for remaining floor
        // dp[K - 1][i - 1] or it doesn't that we use dp[K][N - i]. For each case, we
        // are expecting the worst cast, so the max of them + 1 will be compared with
        // current answer;
        int res = Integer.MAX_VALUE;
        for (int i = 1; i <= N; i++) {
            res = Math.min(res, Math.max(dp(memo, K - 1, i - 1), dp(memo, K, N - i)) + 1);
        }
        memo[K][N] = res;
        return res;
    }
}
```

```java
class Solution {
    public int superEggDrop(int K, int N) {
        int[][] memo = new int[K + 1][N + 1];
        // define memo[i][j] to be the number of moves for i eggs and j floors
        return dp(memo, K, N);
    }
    
    private int dp(int[][] memo, int K, int N) {
        if (N <= 1) return 1;
        if (K == 1) return N;
        if (memo[K][N] > 0) return memo[K][N];
        int res = N;
        int lo = 1, hi = N;
        while (lo < hi) {
            int mi = lo + (hi - lo) / 2;
            int breakMove = dp(memo, K - 1, mi - 1);
            int safeMove = dp(memo, K, N - mi);
            res = Math.min(res, Math.max(breakMove, safeMove) + 1);
            if (breakMove == safeMove) break;
            else if (breakMove > safeMove) hi = mi;
            else lo = mi + 1;
        }
        memo[K][N] = res;
        return res;
    }
}
```

```java
class Solution {
    public int superEggDrop(int K, int N) {
        int[][] dp = new int[K + 1][N + 1];
        for (int j = 1; j <= N; j++) {
            dp[1][j] = j;
        }
        for (int k = 2; k <= K; k++) {
            int x = 1;
            for (int n = 1; n <= N; n++) {
                while (x < n && Math.max(dp[k - 1][x - 1], dp[k][n - x]) > Math.max(dp[k -1][x], dp[k][n - x -1])) x++;
                dp[k][n] = 1 + Math.max(dp[k - 1][x - 1], dp[k][n - x]);
            }
        }
        return dp[K][N];
    }
}
```

```text
class Solution {
    public int superEggDrop(int K, int N) {
        int[][] dp = new int[N + 1][K + 1];
        int m = 0;
        while (dp[m][K] < N) {
            m++;
            for (int k = 1; k <= K; k++) {
                dp[m][k] = dp[m - 1][k - 1] + dp[m - 1][k] + 1;
            }
        }
        return m;
    }
}
```

```java
class Solution {
    public int superEggDrop(int K, int N) {
        int[] dp = new int[K + 1];
        int m = 0;
        while (dp[K] < N) {
            m++;
            for (int k = K; k > 0; k--) {
                dp[k] += dp[k - 1] + 1;
            }
        }
        return m;
    }
}
```

## Additional {#additional}


### Question {#question}

[https://leetcode.com/problems/best-time-to-buy-and-sell-stock-iii/description/](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-iii/description/)

Say you have an array for which the ith element is the price of a given stock on day i.

Design an algorithm to find the maximum profit. You may complete at most two transactions.

**Note:**

You may not engage in multiple transactions at the same time \(ie, you must sell the stock before you buy again\).

**Example:**

```

```

### Thought Process {#thought-process}

1. DP
   1. Create an array of dp, and dp\[k\]\[i\] denotes the maximum profit for kth transaction on selling at ith prices
   2. dp\[k\]\[i\] = max\(dp\[k\]\[i - 1\], maxBuy + prices\[i\]\), which mean the maximum at kth transaction selling at prices i is either the previous profit or the max profit of buying at last prices and sell at current price. And maxBuy = max\(dp\[k - 1\]\[i - 1\] - prices\[i - 1\], dp\[k - 1\]\[i\] - prices\[i\]\), which mean the best profit at buying at previous price on current price
   3. Time complexity O\(kn\), where k is number of transaction allowed and n is number of prices
   4. Space complexity O\(kn\)
2. Optimized Space \(generalized to K transactions\)
   1. Observed the use of two dimensional array is not required
   2. We can save the profit from the last transaction before we update it
   3. Time complexity O\(kn\)
   4. Space complexity O\(n\)
3. Further reduced space
   1. Let's define four variable, buy1, hold1, buy2, hold and each represent the profit after purchase the first stock, sell the first stock, purchase the second stock, and sell the second stock
   2. Each transaction is associated with previous transaction and their formula can be defined below. Negative prices denotes losing money on buying stock and maximum of that denotes the minimum prices used to purchase
   3. buy1\[i\] = max\(buy1\[i- 1\], -prices\[i\]\)
   4. sell1\[i\] = max\(sell1\[i - 1\], buy1\[i - 1\] + prices\[i\]\)
   5. buy2\[i\] = max\(buy2\[i- 1\], sell1\[i - 1\] - prices\[i\]\)
   6. sell2\[i\] = max\(sell2\[i - 1\], buy2\[i - 1\] + prices\[i\]\)
   7. Although we can keep the order, explained here [https://leetcode.com/problems/best-time-to-buy-and-sell-stock-iii/discuss/39615/My-explanation-for-O\(N\)-solution!](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-iii/discuss/39615/My-explanation-for-O%28N%29-solution!), we are better off with order in this order sell2, buy2, sell1, buy1
   8. Time complexity O\(n\)
   9. Space complexity O\(1\)

### Solution

```java
class Solution {
    public int maxProfit(int[] prices) {
        if (prices.length < 2) return 0;
        int K = 2, n = prices.length;
        int[][] dp = new int[K + 1][n];
        // dp[k][i] is the maximum profit for kth transcation for selling at ith prices
        for (int k = 1; k <= K; k++) {
            int buy = dp[k -1][0] - prices[0];
            for (int i = 1; i < n; i++) {
                // buy is the best profit for k - 1 transcation on buying at i - 1 price
                dp[k][i] = Math.max(dp[k][i - 1], buy + prices[i]);
                buy = Math.max(buy, dp[k - 1][i] - prices[i]);
            }
        }
        return dp[K][n - 1];
    }
}
```

```java
class Solution {
    public int maxProfit(int[] prices) {
        if (prices.length < 2) return 0;
        int K = 2, n = prices.length;
        int[] dp = new int[n];
        for (int k = 1; k <= K; k++) {
            int buy = dp[0] - prices[0];
            for (int i = 1; i < n; i++) {
                int lastProfit = dp[i];
                dp[i] = Math.max(dp[i - 1], buy + prices[i]);
                buy = Math.max(buy, lastProfit - prices[i]);
            }
        }
        return dp[n - 1];
    }
}
```

```java
class Solution {
    public int maxProfit(int[] prices) {
        int buy1 = Integer.MIN_VALUE, buy2 = Integer.MIN_VALUE;
        int sell1 = 0, sell2 = 0;
        for (int price : prices) {
            sell2 = Math.max(sell2, buy2 + price);
            buy2 = Math.max(buy2, sell1 - price);
            sell1 = Math.max(sell1, buy1 + price);
            buy1 = Math.max(buy1, -price);
        }
        return sell2;
    }
}
```

### Additional




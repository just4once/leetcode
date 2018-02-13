### Question {#question}

Say you have an array for which the ith element is the price of a given stock on day i.

Design an algorithm to find the maximum profit. You may complete as many transactions as you like \(ie, buy one and sell one share of the stock multiple times\). However, you may not engage in multiple transactions at the same time \(ie, you must sell the stock before you buy again\).

**Example:**

```

```

### Thought Process {#thought-process}

1. First we need to find the local min, then the next local max
   1. repeat the local min and max process until we reach the end
   2. Time complexity O\(n\)
   3. Space complexity O\(1\)
2. Greedy approach
   1. Instead of trying to find local min and local max, we can pretend that we can buy and sell at the same day, this transaction can be treated as gathering profit as we go
   2. Anytime that the stock price is higher than the yesterday's, we gather out profit, this is essentially same as the buy at the lowest price and sell at the highest price
   3. Time complexity O\(n\)
   4. Space complexity O\(1\)

### Solution

```java
class Solution {
    public int maxProfit(int[] prices) {
        int profit = 0;
        for (int i = 1; i < prices.length; i++){
            if (prices[i] > prices[i - 1]) profit += prices[i] - prices[i -1];
        }
        return profit;
    }
}
```

### Additional {#additional}




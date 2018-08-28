# 121-best-time-to-buy-and-sell-stock

## Question {#question}

[https://leetcode.com/problems/best-time-to-buy-and-sell-stock/description/](https://leetcode.com/problems/best-time-to-buy-and-sell-stock/description/)

Say you have an array for which the ith element is the price of a given stock on day i.

If you were only permitted to complete at most one transaction \(ie, buy one and sell one share of the stock\), design an algorithm to find the maximum profit.

**Example 1:**

```text
Input: [7, 1, 5, 3, 6, 4]
Output: 5

max. difference = 6-1 = 5 (not 7-1 = 6, as selling price needs to be larger than buying price)
```

**Example 2:**

```text
Input: [7, 6, 4, 3, 1]
Output: 0

In this case, no transaction is done, i.e. max profit = 0.
```

## Thought Process {#thought-process}

1. As we loop through all the elements, we need to compare each element to the previous known min
   1. If we find a smaller element, we need to set it to min, because we will have larger profit buying this stock
   2. Else we can potential make a profit now
   3. Time complexity O\(n\)
   4. Space complexity O\(1\)
2. This can also be treated as max subarray sum
   1. When selling at cur price make the sum go below 0, we reset it to 0
   2. We also keep track of max of the sum to make sure to we get the max profit
   3. Time complexity O\(n\)
   4. Space complexity O\(1\)

## Solution

```java
class Solution {
    public int maxProfit(int[] prices) {
        // if cur price is smaller than min, we should set it to min
        // and get a better profit buying this stock 
        int min = Integer.MAX_VALUE, profit = 0;
        for (int i = 0; i < prices.length; i++) {
            if (prices[i] < min) min = prices[i];
            else profit = Math.max(prices[i] - min, profit);
        }
        return profit;
    }
}
```

```java
class Solution {
    public int maxProfit(int[] prices) {
        int maxCur = 0, maxSoFar = 0;
        for(int i = 1; i < prices.length; i++) {
            maxCur = Math.max(0, maxCur += prices[i] - prices[i-1]);
            maxSoFar = Math.max(maxCur, maxSoFar);
        }
        return maxSoFar;
    }
}
```

## Additional {#additional}


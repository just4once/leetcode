### Question {#question}

[https://leetcode.com/problems/arranging-coins/description/](https://leetcode.com/problems/arranging-coins/description/)

You have a total of n coins that you want to form in a staircase shape, where every k-th row must have exactly k coins.

Givenn, find the total number of **full **staircase rows that can be formed.

n is a non-negative integer and fits within the range of a 32-bit signed integer.

**Example 1:**

```
n = 5

The coins can form the following rows:
¤
¤ ¤
¤ ¤

Because the 3rd row is incomplete, we return 2.
```

**Example 2:**

```
n = 8

The coins can form the following rows:
¤
¤ ¤
¤ ¤ ¤
¤ ¤

Because the 4th row is incomplete, we return 3.
```

### Thought Process {#thought-process}

1. Brute Force
   1. Simply deduct from 1 to n, where we try to get as many levels as possible
   2. Time complexity O\(n^0.5\)
   3. Space complexity O\(1\)
2. Binary Search \(Gauss Formula\)
   1. Since each level contains corresponding number of coins, we can use Gauss formula to find how many level we need
   2. Let's assume that the we need x level, we will have x\(x + 1\)/2 &lt;= n
   3. We declare lo = 1 and hi = n, and perform binary search until we have reach the end
   4. Obviously if mid\(mid + 1\) is equal to 2n, we can return it
   5. If mid\(mid + 1\) &lt; 2n, 
3. asd

### Solution

```java
class Solution {
    public int arrangeCoins(int n) {
        int level = 0, coin = 1;
        while (n >= coin) {
            n -= coin;
            coin++;
            level++;
        }
        return level;
    }
}
```

```java
class Solution {
    public int arrangeCoins(int n) {
        int lo = 1, hi = n, mid;
        while (lo <= hi) {
            mid = lo + (hi - lo) / 2;
            if (mid * (mid + 1L) <= n * 2L) lo = mid + 1;
            else hi = mid - 1;
        }
        return hi;
    }
}
```

### Additional {#additional}




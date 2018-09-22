# 875-koko-eating-bananas

## Question {#question}

\*\*\*\*[**https://leetcode.com/problems/koko-eating-bananas/description/**](https://leetcode.com/problems/koko-eating-bananas/description/)\*\*\*\*

Koko loves to eat bananas.  There are `N` piles of bananas, the `i`-th pile has `piles[i]` bananas.  The guards have gone and will come back in `H` hours.

Koko can decide her bananas-per-hour eating speed of `K`.  Each hour, she chooses some pile of bananas, and eats K bananas from that pile.  If the pile has less than `K` bananas, she eats all of them instead, and won't eat any more bananas during this hour.

Koko likes to eat slowly, but still wants to finish eating all the bananas before the guards come back.

Return the minimum integer `K` such that she can eat all the bananas within `H` hours.

* 
**Example 1:**

```text
Input: piles = [3,6,7,11], H = 8
Output: 4
```

**Example 2:**

```text
Input: piles = [30,11,23,4,20], H = 5
Output: 30
```

**Example 3:**

```text
Input: piles = [30,11,23,4,20], H = 6
Output: 23
```

**Note:**

* `1 <= piles.length <= 10^4`
* `piles.length <= H <= 10^9`
* `1 <= piles[i] <= 10^9`

## Thought Process {#thought-process}

1. Binary Search
   1. Since the time is bounded by 1 and 10e9, we can successively half our search, lo and hi respectively
   2. When the function canFinish\(mi\), we set our hi = mi, else we can increase our speed, so lo = mi + 1
   3. Time complexity O\(nlog\(w\)\), where w is the range and n is number of elements
   4. Space complexity O\(1\)
2. Search Starts from Average Speed
   1. Instead of making guess, we can smartly guess our initial value to be sum / H
   2. If the speed is not enough, we can increase speed by 1 until Koko can finish it
   3. Time complexity O\(n\)
   4. Space complexity O\(1\)

## Solution

```java
class Solution {
    public int minEatingSpeed(int[] piles, int H) {
        int lo = 1, hi = 1000000000;
        while (lo < hi) {
            int mi = lo + (hi - lo) / 2;
            if (canFinish(piles, mi, H)) hi = mi;
            else lo = mi + 1;
        }
        return lo;
    }
    
    private boolean canFinish(int[] piles, int K, int H) {
        int hour = 0;
        for (int pile : piles) {
            hour += (pile - 1) / K + 1;
        }
        return hour <= H;
    }
}
```

```java
class Solution {
    public int minEatingSpeed(int[] piles, int H) {
        long sum = 0;
        for (int pile : piles) sum += pile;
        long speed = (sum - 1) / H + 1L;
        while (true) {
            if (canFinish(piles, speed, H)) return (int) speed;
            else speed++;
        }
    }
    
    private boolean canFinish(int[] piles, long K, int H) {
        int hour = 0;
        for (int pile : piles) {
            hour += (pile - 1) / K + 1;
        }
        return hour <= H;
    }
}
```

## Additional {#additional}


# 862-shortest-subarray-with-sum-at-least-k

## Question {#question}

[https://leetcode.com/problems/shortest-subarray-with-sum-at-least-k/description/](https://leetcode.com/problems/shortest-subarray-with-sum-at-least-k/description/)

Return the length of the shortest, non-empty, contiguous subarray of A with sum at least K.

If there is no non-empty subarray with sum at least K, return -1.

**Example 1:**

```text
Input: A = [1], K = 1
Output: 1
```

**Example 2:**

```text
Input: A = [1,2], K = 4
Output: -1
```

**Example 3:**

```text
Input: A = [2,-1,2], K = 3
Output: 3
```

**Note:**

* 1 &lt;= A.length &lt;= 50000
* -10 ^ 5 &lt;= A\[i\] &lt;= 10 ^ 5
* 1 &lt;= K &lt;= 10 ^ 9

## Thought Process {#thought-process}

1. Deque
   1. This problem can be rephrased as prefix sums of A, let's call it P
   2. For every index j, we are trying to find largest i such that P\[j\] - P\[i\] &gt;= K
   3. If we check all the prefix sums before j, the run time will become n^2
   4. For every j we visited, we add it to queue as potential answer for next j, let's define Q\[0\] to be the 1st item and Q\[1\] to be 2nd item and the rest follows the same pattern
   5. For current j, we compare P\[j\] to P\[Q\[0\]\] and check if their difference &gt;= K
   6. If the difference is &gt;= K, we can pop the first item because the in the next iteration, the length of using the first item will not be any better than current length
   7. Another observation is that if P\[j\] is &lt;= P\[Q\[last\]\], it's a better candidate than the last deque element, therefore we use while loop to removeLast
   8. Essentially, we are maintaining a increasing P\[i\] in the deque
   9. Time complexity O\(n\)
   10. Space complexity O\(n\) 

## Solution

```java
class Solution {
    public int shortestSubarray(int[] A, int K) {
        int n = A.length;
        int[] P = new int[n + 1];
        for(int i = 1; i < P.length; i++) P[i] = P[i - 1] + A[i - 1];
        Deque<Integer> deque = new LinkedList<>();
        int res = n + 1;
        for (int j = 0; j < P.length; j++) {
            while (!deque.isEmpty() && P[j] - P[deque.getFirst()] >= K) res = Math.min(res, j - deque.removeFirst());
            while (!deque.isEmpty() && P[j] <= P[deque.getLast()]) deque.pollLast();
            deque.offer(j);
        }
        return res == n + 1 ? - 1 : res;
    }
}
```

## Additional {#additional}


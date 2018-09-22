# 786-k-th-smallest-prime-fraction

## Question {#question}

[https://leetcode.com/problems/k-th-smallest-prime-fraction/description/](https://leetcode.com/problems/k-th-smallest-prime-fraction/description/)

A sorted list A contains 1, plus some number of primes. Then, for every p &lt; q in the list, we consider the fraction p/q.

What is the K-th smallest fraction considered? Return your answer as an array of ints, where answer\[0\] = p and answer\[1\] = q.

**Example:**

```text
Input: A = [1, 2, 3, 5], K = 3
Output: [2, 5]
Explanation:
The fractions to be considered in sorted order are:
1/5, 1/3, 2/5, 1/2, 3/5, 2/3.
The third fraction is 2/5.

Input: A = [1, 7], K = 1
Output: [1, 7]
```

**Note:**

* A will have length between 2 and 2000.
* Each A\[i\] will be between 1 and 30000.
* K will be between 1 and A.length \* \(A.length - 1\) / 2.

## Thought Process {#thought-process}

1. MinHeap - Brute Force \(TLE\)
   1. Save the dividend p and divisor q into a node
   2. Use priority queue to poll up a node base on the quotient, which = p / q
   3. The Kth node on the heap will the our answer
   4. Time complexity O\(n^2log\(n\)\)
   5. Space complexity O\(n^2\)
2. MaxHeap - Size Control \(TLE\)
   1. Use max heap we can improve the performance
   2. We monitor the size of heap, and poll out biggest one if the heap size is greater than K
   3. Time complexity O\(n^2log\(K\)\)
   4. Space complexity O\(K\)
3. MinHeap
   1. Instead of checking all the combinations, we smartly add the next smallest quotient
   2. We create the node to store the indices of dividend and divisor
   3. Every time, we poll out a min node, we slide the divisor forward until the dividend's next number
   4. Time complexity O\(nlog\(n\)\)
   5. Space complexity O\(n\)
4. asdsad

## Solution

```java
class Solution {
    public class Node {
        int p, q;
        Node (int p, int q) {
            this.p = p;
            this.q = q;
        }
    }
    
    public int[] kthSmallestPrimeFraction(int[] A, int K) {
        PriorityQueue<Node> pq = new PriorityQueue<>((a, b) -> a.p * 1.0 / a.q > b.p * 1.0 / b.q ? 1 : -1);
        for (int i = 0; i < A.length - 1; i++) {
            for (int j = i + 1; j < A.length; j++) {
                pq.offer(new Node(A[i], A[j]));
            }
        }
        while (--K > 0) pq.poll();
        int[] res = {pq.peek().p, pq.peek().q};
        return res;
    }
}
```

## Additional {#additional}


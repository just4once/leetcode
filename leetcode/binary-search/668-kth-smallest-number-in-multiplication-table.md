# 668-kth-smallest-number-in-multiplication-table

## Question {#question}

[https://leetcode.com/problems/kth-smallest-number-in-multiplication-table/description/](https://leetcode.com/problems/kth-smallest-number-in-multiplication-table/description/)

Nearly every one have used the [Multiplication Table](https://en.wikipedia.org/wiki/Multiplication_table). But could you find out the `k-th` smallest number quickly from the multiplication table?

Given the height`m`and the length`n`of a`m * n` Multiplication Table, and a positive integer`k`, you need to return the `k-th` smallest number in this table.

**Example 1:**

```text
Input: m = 3, n = 3, k = 5
Output: 
Explanation: 
The Multiplication Table:
1    2    3
2    4    6
3    6    9

The 5-th smallest number is 3 (1, 2, 2, 3, 3).
```

**Example 2:**

```text
Input: m = 2, n = 3, k = 6
Output: 
Explanation: 
The Multiplication Table:
1    2    3
2    4    6

The 6-th smallest number is 6 (1, 2, 2, 3, 4, 6).
```

**Note:**

1. The m and n will be in the range \[1, 30000\].
2. The k will be in the range \[1, m \* n\]

## Thought Process {#thought-process}

1. Brute Force \(TLE\)
   1. Create all the products and save them into an array and sort them
   2. Time complexity O\(mnlog\(mn\)\)
   3. Space complexity O\(mn\)
2. Heap \(TLE\)
   1. Create an max heap of size k, then we can pop the largest element as we loop through our products
   2. Time complexity O\(mnlog\(k\)\)
   3. Space complexity O\(k\)
3. Heap2 \(TLE\)
   1. Use minHeap to store nodes, where each node contains the value and its row
   2. As we loop through the heap k times, we insert the next node with value and row appropiately
   3. Time complexity O\(klogm + mlogm\)
   4. Space complexity O\(m\)
4. Binary Search
   1. Perform binary search on values ranging from 1 to mn, named lo and hi respectively, and mid is our x
   2. We also need another function enough to check if x is good enough to be our answer.
   3. In other words, we are checking if there are k \(or more\) numbers of values less than x, count\(&lt;=x\) &gt;= k
   4. If enough\(x\) returns false that means x is too small, our answer has to be larger than x, so lo = mid + 1
   5. Else this x could our potential answer, so we set hi = mid
   6. Inside the enough function, we have a while loop to go through the rows to get the numbers of values greater than x, which can be calculate by sum of min\(n, x / i\), where i is the row
   7. Time complexity O\(log\(mn\)m\)

## Solution

Brute Force

```java
class Solution {
    public int findKthNumber(int m, int n, int k) {
        int[] products = new int[m * n];
        int x = 0;
        for (int i = 1; i <= m; i++) {
            for (int j = 1; j <= n; j++) {
                products[x++] = i * j;
            }
        }
        Arrays.sort(products);
        return products[k - 1];
    }
}
```

Heap1

```java
class Solution {
    public int findKthNumber(int m, int n, int k) {
        PriorityQueue<Integer> maxHeap = new PriorityQueue<>((a, b) -> b - a);
        for (int i = 1; i <= m; i++) {
            for (int j = 1; j <= n; j++) {
                maxHeap.offer(i * j);
                if (maxHeap.size() > k) maxHeap.poll();
            }
        }
        return maxHeap.peek();
    }
}
```

Heap2

```java
class Solution {
    private class Node implements Comparable<Node> {
        int val, row;
        public Node(int val, int row) {
            this.val = val;
            this.row = row;
        }

        public int compareTo(Node that) {
            return this.val - that.val;
        }
    }

    public int findKthNumber(int m, int n, int k) {
        PriorityQueue<Node> minHeap = new PriorityQueue<>();
        for (int i = 1; i <= m; i++) minHeap.offer(new Node(i, i));
        Node cur = null;
        for (int i = 1; i <= k; i++) {
            cur = minHeap.poll();
            if (cur.val + cur.row <= cur.row * n) minHeap.offer(new Node(cur.val + cur.row, cur.row));
        }
        return cur.val;
    }
}
```

Binary

```java
class Solution {
    public int findKthNumber(int m, int n, int k) {
        int lo = 1, hi = m * n;
        while (lo < hi) {
            int mi = lo + (hi - lo) / 2;
            if (!enough(m, n, k, mi)) lo = mi + 1;
            else hi = mi;
        }
        return lo;
    }

    private boolean enough(int m, int n, int k, int x) {
        int count = 0;
        for (int i = 1; i <= m; i++) {
            count += Math.min(x / i, n);
        }
        return count >= k;
    }
}
```

## Additional {#additional}


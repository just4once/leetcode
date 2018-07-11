### Question {#question}

[https://leetcode.com/problems/kth-smallest-number-in-multiplication-table/description/](https://leetcode.com/problems/kth-smallest-number-in-multiplication-table/description/)

Nearly every one have used the [Multiplication Table](https://en.wikipedia.org/wiki/Multiplication_table). But could you find out the `k-th` smallest number quickly from the multiplication table?

Given the height`m`and the length`n`of a`m * n` Multiplication Table, and a positive integer`k`, you need to return the `k-th` smallest number in this table.

**Example 1:**

```
Input: m = 3, n = 3, k = 5
Output: 
Explanation: 
The Multiplication Table:
1	2	3
2	4	6
3	6	9

The 5-th smallest number is 3 (1, 2, 2, 3, 3).
```

**Example 2:**

```
Input: m = 2, n = 3, k = 6
Output: 
Explanation: 
The Multiplication Table:
1	2	3
2	4	6

The 6-th smallest number is 6 (1, 2, 2, 3, 4, 6).
```

**Note:**

1. The m and n will be in the range \[1, 30000\].
2. The k will be in the range \[1, m \* n\]

### Thought Process {#thought-process}

1. Brute Force \(TLE\)
   1. Create all the products and save them into an array and sort them
   2. Time complexity O\(mnlog\(mn\)\)
   3. Space complexity O\(mn\)
2. Heap
   1. Create an max heap of size k, then we can pop the largest element as we loop through our products
   2. Time complexity O\(mnlog\(k\)\)
   3. Space complexity O\(k\)
3. Heap2
   1. Use minHeap to store the node, where node contains the current value and its respective row
   2. We store the nodes based on their value
   3. 
4. asd

### Solution

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

### Additional {#additional}




### Question {#question}

[https://leetcode.com/problems/max-sum-of-rectangle-no-larger-than-k/description/](https://leetcode.com/problems/max-sum-of-rectangle-no-larger-than-k/description/)

Given a non-empty 2D matrix matrix and an integer k, find the max sum of a rectangle in the matrix such that its sum is no larger than k.

**Example:**

```
Given matrix = [
  [1,  0, 1],
  [0, -2, 3]
]
k = 2
```

The answer is 2. Because the sum of rectangle \[\[0, 1\], \[-2, 3\]\] is 2 and 2 is the max number no larger than k \(k = 2\).

**Note:**

1. The rectangle inside the matrix must have an area &gt; 0.
2. What if the number of rows is much larger than the number of columns?

### Thought Process {#thought-process}

1. Presum and Binary Search
   1. We need a way to get all the rectangles, which can be define by 4 variables r1, r2, c1 c2 that means the top row, bottom row, left column and right column
   2. Unlike brute force that requires time complexity O\(m^2n^2\), we can use built-in TreeSet to find the ceilling of \(currentSum - k\)
   3. Adding partial sum ending at column and r2, we can do binary search on 
   4. Time complexity O\(m^2nlogn\)
   5. Space complexity O\(n\)

### Solution

```java
class Solution {
    public int maxSumSubmatrix(int[][] matrix, int k) {
        int m = matrix.length, n = matrix[0].length;
        int res = Integer.MIN_VALUE;
        for (int r1 = 0; r1 < m; r1++) {
            int[] presum = new int[n];
            for (int r2 = r1; r2 < m; r2++) {
                TreeSet<Integer> set = new TreeSet<Integer>();
                set.add(0);
                int val = 0;
                for (int c = 0; c < n; c++) {
                    presum[c] += matrix[r2][c];
                    val += presum[c];
                    Integer prev = set.ceiling(val - k);
                    if (prev != null) {
                        res = Math.max(res, val - prev);
                    }
                    set.add(val);
                }
            }
        }
        return res;
    }
}
```

```java
class Solution {
    public int maxSumSubmatrix(int[][] matrix, int k) {
        int m = matrix.length, n = matrix[0].length;
        int res = Integer.MIN_VALUE;
        for (int c1 = 0; c1 < n; c1++) {
            int[] presum = new int[m];
            for (int c2 = c1; c2 < n; c2++) {
                TreeSet<Integer> set = new TreeSet<Integer>();
                set.add(0);
                int val = 0;
                for (int r = 0; r < m; r++) {
                    presum[r] += matrix[r][c2];
                    val += presum[r];
                    Integer prev = set.ceiling(val - k);
                    if (prev != null) {
                        res = Math.max(res, val - prev);
                    }
                    set.add(val);
                }
            }
        }
        return res;
    }
}
```

### Additional {#additional}




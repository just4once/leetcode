# 073-set-matrix-zeroes

## Question {#question}

[https://leetcode.com/problems/set-matrix-zeroes/description/](https://leetcode.com/problems/set-matrix-zeroes/description/)

Given a m x n matrix, if an element is 0, set its entire row and column to 0. Do it in place.

**Example:**

```text

```

## Thought Process {#thought-process}

1. We can use an extra array in a separate array
   1. Time complexity O\(mn\)
   2. Space complexity O\(mn\)
2. We can directly record the state in the first row and first column,
   1. The first record decide whether this column should be zero or not and first column decide whether current row should be zero or not
   2. One thing that we need to keep in mind that, we need to keep one of indicator either the first row and first column in tact to preserve the information

## Solution

```java
class Solution {
    public void setZeroes(int[][] matrix) {
        if (matrix == null || matrix.length == 0) return;
        int m = matrix.length, n = matrix[0].length;
        boolean isFirstColZero = false;
        for (int r = 0; r < m; r++) {
            if (matrix[r][0] == 0) isFirstColZero = true;
            // skip the column 0 to save the info for each row
            for (int c = 1; c < n; c++) {
                if (matrix[r][c] == 0) {
                    matrix[0][c] = matrix[r][0] = 0;
                }
            }
        }
        for (int r = m - 1; r >= 0; r--) {
            for (int c = n - 1; c > 0; c--) {
                if (matrix[0][c] == 0 || matrix[r][0] == 0) {
                    matrix[r][c] = 0;
                }
            }
            if (isFirstColZero) matrix[r][0] = 0;
        }
    }
}
```

## Additional {#additional}


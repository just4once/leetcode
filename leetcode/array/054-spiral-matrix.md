# 054-spiral-matrix

## Question {#question}

[https://leetcode.com/problems/spiral-matrix/description/](https://leetcode.com/problems/spiral-matrix/description/)

Given a matrix of m x n elements \(m rows, n columns\), return all elements of the matrix in spiral order.

**Example:**

Given the following matrix:

```text
[
 [ 1, 2, 3 ],
 [ 4, 5, 6 ],
 [ 7, 8, 9 ]
]
```

You should return`[1,2,3,6,9,8,7,4,5]`.

## Thought Process {#thought-process}

1. Collect in the order top, right, bottom, left
2. We go from outer layer inward
3. Time complexity O\(n\)
4. Space complexity O\(n\), O\(1\) extra space

## Solution

```java
class Solution {
    public List<Integer> spiralOrder(int[][] matrix) {
        List<Integer> res = new ArrayList<>();
        if (matrix == null || matrix.length == 0) return res;
        int m = matrix.length, n = matrix[0].length;
        int top = 0, bottom = m - 1;
        int left = 0, right = n - 1;
        while (top <= bottom && left <= right) {
            // collect the top row
            for (int c = left; c <= right; c++) res.add(matrix[top][c]);
            top++;
            // collect the right column
            for (int r = top; r <= bottom; r++) res.add(matrix[r][right]);
            right--;
            // collect the bottom row
            for (int c = right; c >= left; c--) res.add(matrix[bottom][c]);
            bottom--;
            // collect the left column
            for (int r = bottom; r >= top; r--) res.add(matrix[r][left]);
            left++;
        }
        return res;
    }
}
```

## Additional {#additional}


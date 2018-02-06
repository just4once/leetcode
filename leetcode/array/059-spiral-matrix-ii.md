### Question {#question}

[https://leetcode.com/problems/spiral-matrix-ii/description/](https://leetcode.com/problems/spiral-matrix-ii/description/)

Given an integer n, generate a square matrix filled with elements from 1 to n2 in spiral order.

**Example:**

```
Given n = 3,
You should return the following matrix:
[
 [ 1, 2, 3 ],
 [ 8, 9, 4 ],
 [ 7, 6, 5 ]
]
```

### Thought Process {#thought-process}

1. Very similar to [054-Spiral Matrix](/leetcode/array/054-spiral-matrix.md), we can reuse very much the same code
2. Fill the top, right, bottom, and left
3. Time complexity O\(n^2\)
4. Space complexity O\(n^2\), O\(1\) extra

### Solution

```java
class Solution {
    public int[][] generateMatrix(int n) {
        int[][] result = new int[n][n];
        int left = 0, right = n - 1;
        int top = 0, bottom = n - 1;
        int count = 1;
        while(left <=right && top <= bottom){
            // fill the top
            for(int col = left; col <= right; col++){
                result[top][col] = count++;
            }
            top++;
            // fill the right
            for(int row = top; row <= bottom; row++){
                result[row][right] = count++;
            }
            right--;
            // fill the bottom
            for(int col = right; col >= left; col--){
                result[bottom][col] = count++;
            }
            bottom--;
            // fill the left
            for(int row = bottom; row >= top; row--){
                result[row][left] = count++;
            }
            left++;
        }
        return result;
    }
}
```

### Additional {#additional}




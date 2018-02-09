### Question {#question}

Given a 2D binary matrix filled with 0's and 1's, find the largest rectangle containing only 1's and return its area.

**Example:**

```markdown
1 0 1 0 0
1 0 1 1 1
1 1 1 1 1
1 0 0 1 0

Return 6.
```

### Thought Process {#thought-process}

1. This is very similar to , instead of giving heights directly to us, we have to computer row by row. Therefore we need an additional array to hold the heights of the column
2. Time complexity O\(n^2\)
3. Space complexity O\(n\)

### Solution

```java
class Solution {
    public int maximalRectangle(char[][] matrix) {
        if (matrix == null || matrix.length == 0) return 0;
        int n = matrix[0].length;
        int[] heights = new int[n + 1];
        int maxArea = 0;
        for (char[] row : matrix) {
            updateHeight(row, heights);
            maxArea = Math.max(maxArea, getMaxArea(heights));
        }
        return maxArea;
    }
    
    private void updateHeight(char[] row, int[] heights) {
        for (int i = 0; i < row.length; i++) {
            if (row[i] == '1') heights[i]++;
            else heights[i] = 0;
        }
    }
    
    private int getMaxArea(int[] heights) {
        int n = heights.length;
        int[] stack = new int[n + 1];
        int top = 0;
        stack[top] = -1;
        int maxArea = 0;
        for (int i = 0; i < n; i++) {
            while (top > 0 && heights[i] < heights[stack[top]]) {
                int h = heights[stack[top--]];
                int w = i - stack[top] - 1;
                maxArea = Math.max(maxArea, h * w);
            }
            stack[++top] = i;
        }
        return maxArea;
    }
}
```

### Additional {#additional}




### Question {#question}

[https://leetcode.com/problems/smallest-rectangle-enclosing-black-pixels/description/](https://leetcode.com/problems/smallest-rectangle-enclosing-black-pixels/description/)

An image is represented by a binary matrix with 0 as a white pixel and 1 as a black pixel. The black pixels are connected, i.e., there is only one black region. Pixels are connected horizontally and vertically. Given the location \(x, y\) of one of the black pixels, return the area of the smallest \(axis-aligned\) rectangle that encloses all black pixels.

**Example:**

```
[
  "0010",
  "0110",
  "0100"
]

and x = 0, y = 2,
Return 6.
```

### Thought Process {#thought-process}

1. Linear Scan
   1. Doing linear scan over the whole map, we can find the minimum top and left and maximum bottom and right
   2. Then the area = \(right - left + 1\) x \(bottom - top + 1\)
   3. Time complexity O\(mn\)
   4. Space complexity O\(1\)
2. DFS
   1. By using recursion, we can travel to four directions and marked visited cell '0'
   2. Time complexity O\(E\), where E is number of edges, in worst case O\(mn\)
   3. Space complexity O\(V\), where V is number of vertices, in worst case O\(mn\)
3. ASD

### Solution

```java
class Solution {
    public int minArea(char[][] image, int x, int y) {
        if (image.length == 0 || image[0].length == 0) return 0;
        int m = image.length, n = image[0].length;
        int top = x, bottom = x, left = y, right = y;
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                if (image[i][j] == '1') {
                    top = Math.min(top, i);
                    bottom = Math.max(bottom, i);
                    left = Math.min(left, j);
                    right = Math.max(right, j);
                }
            }
        }
        return (right - left + 1) * (bottom - top + 1);
    }
}
```

```java
class Solution {
    private int top, bottom, left, right;
    public int minArea(char[][] image, int x, int y) {
        if (image.length == 0 || image[0].length == 0) return 0;
        top = bottom = x;
        left = right = y;
        dfs(image, x, y);
        return (right - left + 1) * (bottom - top + 1);
    }
    
    private void dfs(char[][] image, int i, int j) {
        if (i < 0 || i >= image.length || j < 0 || j >= image[0].length || image[i][j] == '0') return;
        top = Math.min(top, i);
        bottom = Math.max(bottom, i);
        left = Math.min(left, j);
        right = Math.max(right, j);
        image[i][j] = '0';
        dfs(image, i - 1, j);
        dfs(image, i + 1, j);
        dfs(image, i, j - 1);
        dfs(image, i, j + 1);
    }
}
```

### Additional {#additional}




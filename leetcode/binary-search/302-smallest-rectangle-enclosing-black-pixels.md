# 302-smallest-rectangle-enclosing-black-pixels

## Question {#question}

[https://leetcode.com/problems/smallest-rectangle-enclosing-black-pixels/description/](https://leetcode.com/problems/smallest-rectangle-enclosing-black-pixels/description/)

An image is represented by a binary matrix with 0 as a white pixel and 1 as a black pixel. The black pixels are connected, i.e., there is only one black region. Pixels are connected horizontally and vertically. Given the location \(x, y\) of one of the black pixels, return the area of the smallest \(axis-aligned\) rectangle that encloses all black pixels.

**Example:**

```text
[
  "0010",
  "0110",
  "0100"
]

and x = 0, y = 2,
Return 6.
```

## Thought Process {#thought-process}

1. Linear Scan
   1. Doing linear scan over the whole map, we can find the minimum top and left and maximum bottom and right
   2. Then the area = \(right - left + 1\) x \(bottom - top + 1\)
   3. Time complexity O\(mn\)
   4. Space complexity O\(1\)
2. DFS
   1. By using recursion, we can travel to four directions and marked visited cell '0'
   2. Time complexity O\(E\) = O\(B\), where E is number of edges, B is number of black pixels, in worst case O\(mn\)
   3. Space complexity O\(V\) = O\(B\), where V is number of vertices, in worst case O\(mn\)
3. Binary Search
   1. To search the boundaries, we can actually use the binary search by looping through all the rows and columns for left and right, and top and bottom respectively
   2. To find the left and right boundary, we need to limit the search \[0, y\), and \[y + 1, n\) respectively
   3. To find the top and bottom boundary, we need to limit the search \[0,x\), and \[x + 1, m\) respectively
   4. Time complexity O\(mlogn + nlogm\)
   5. Space complexity O\(1\)

## Solution

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

```java
class Solution {
    private int top, bottom, left, right;
    public int minArea(char[][] image, int x, int y) {
        if (image.length == 0 || image[0].length == 0) return 0;
        int m = image.length, n = image[0].length;
        int left = searchColumns(image, 0, y, 0, m, true);
        int right = searchColumns(image, y + 1, n, 0, m, false);
        int top = searchRows(image, 0, x, left, right, true);
        int bottom = searchRows(image, x + 1, m, left, right, false);
        return (right - left) * (bottom - top);
    }

    private int searchColumns(char[][] image, int i, int j, int top, int bottom, boolean goLower) {
        while (i < j) {
            int k = top, mid = (i + j) / 2;
            while (k < bottom && image[k][mid] == '0') k++;
            if (k < bottom == goLower) j = mid;
            else i = mid + 1;
        }
        return i;
    }

    private int searchRows(char[][] image, int i, int j, int left, int right, boolean goLower) {
        while (i < j) {
            int k = left, mid = (i + j) / 2;
            while (k < right && image[mid][k] == '0') k++;
            if (k < right == goLower) j = mid;
            else i = mid + 1;
        }
        return i;
    }
}
```

```java
class Solution {
    private int top, bottom, left, right;
    public int minArea(char[][] image, int x, int y) {
        if (image.length == 0 || image[0].length == 0) return 0;
        int m = image.length, n = image[0].length;
        int left = search(image, 0, y, 0, m, true, true);
        int right = search(image, y + 1, n, 0, m, true, false);
        int top = search(image, 0, x, left, right, false, true);
        int bottom = search(image, x + 1, m, left, right, false, false);
        return (right - left) * (bottom - top);
    }

    private int search(char[][] image, int i, int j, int low, int hi, boolean horizontal, boolean goLower) {
        while (i < j) {
            boolean found = false;
            int mid = (i + j) / 2;
            for (int k = low; k < hi && !found; k++) {
                if ((horizontal ? image[k][mid] : image[mid][k]) == '1') {
                    found = true;
                }
            }
            if (found == goLower) j = mid;
            else i = mid + 1;
        }
        return i;
    }
}
```

## Additional {#additional}


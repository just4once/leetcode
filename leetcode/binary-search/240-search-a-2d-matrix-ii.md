### Question {#question}

[https://leetcode.com/problems/search-a-2d-matrix-ii/description/](https://leetcode.com/problems/search-a-2d-matrix-ii/description/)

Write an efficient algorithm that searches for a value in anmxnmatrix. This matrix has the following properties:

* Integers in each row are sorted in ascending from left to right.
* Integers in each column are sorted in ascending from top to bottom.

**Example:**

```
[
  [1,   4,  7, 11, 15],
  [2,   5,  8, 12, 19],
  [3,   6,  9, 16, 22],
  [10, 13, 14, 17, 24],
  [18, 21, 23, 26, 30]
]
```

Given target = 5, return true.

Given target = 20, return false.

### Thought Process {#thought-process}

1. Four Quadrants and Recursion
   1. We can leverage the fact the the top left will be the smallest element and bottom right is largest element to filler out the quadrants that won't contain the target
   2. If the target is smaller than the top left or greater than the bottom right, we know for sure this quadrant will not contain the target
   3. We start from the middle column and search for the cell that is just greater than the target, label this row
   4. Then the quadrant on the top left and bottom bottom right can be ignore because their biggest element are smaller than target and smallest element is greater than target respectively
   5. Master theorem [https://en.wikipedia.org/wiki/Master\_theorem\_\(analysis\_of\_algorithms\)](https://en.wikipedia.org/wiki/Master_theorem_%28analysis_of_algorithms%29)
   6. Time complexity O\(nlogn\)
   7. Space complexity O\(logn\)
2. Top Right to Bottom Left
   1. Since the array is sorted ascendingly from left to right and top to bottom, we use the top right to decide where to go
   2. If the target is smaller than the top right \(i,j\), then the target might be on the left of it
   3. If the target is greater than the top right, then the target might be below it
   4. Time complexity O\(m + n\), because every iteration we move 1 step in one of directions
   5. Space complexity O\(1\)

### Solution

```java
class Solution {
    public boolean searchMatrix(int[][] mat, int targ) {
        if (mat == null || mat.length == 0 || mat[0].length == 0) return false;
        return search(mat, targ, 0, mat.length - 1, 0, mat[0].length - 1);
    }
    
    private boolean search(int[][] mat, int targ, int top, int bottom, int left, int right) {
        if (top > bottom || left > right) return false;
        if (targ < mat[top][left] || targ > mat[bottom][right]) return false;
        int midC = left + (right - left) / 2;
        int midR = top;
        while (midR <= bottom && mat[midR][midC] <= targ) {
            if (mat[midR][midC] == targ) return true;
            midR++;
        }
        return search(mat, targ, midR, bottom, left, midC - 1) || search(mat, targ, top, midR - 1, midC + 1, right);
    }
}
```

```java
class Solution {
    public boolean searchMatrix(int[][] mat, int targ) {
        if (mat == null || mat.length == 0 || mat[0].length == 0) return false;
        int top = 0, right = mat[0].length - 1;
        while (top < mat.length && right >= 0) {
            if (mat[top][right] > targ) right--;
            else if (mat[top][right] < targ) top++;
            else return true;
        }
        return false;
    }
}
```

### Additional {#additional}




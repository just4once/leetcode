### Question {#question}

[https://leetcode.com/problems/search-a-2d-matrix/description/](https://leetcode.com/problems/search-a-2d-matrix/description/)

Write an efficient algorithm that searches for a value in anmxnmatrix. This matrix has the following properties:

* Integers in each row are sorted from left to right.
* The first integer of each row is greater than the last integer of the previous row.

**Example:**

```
[
  [1,   3,  5,  7],
  [10, 11, 16, 20],
  [23, 30, 34, 50]
]
Given target = 3, return true.
```

### Thought Process {#thought-process}

1. We can treat this as one dimensional array, we can perform binary search as well
2. The only difference is the way to calculate the index
3. Time complexity O\(log \(mn\)\)
4. Space complexity O\(1\)

### Solution

```java
class Solution {
    public boolean searchMatrix(int[][] matrix, int target) {
        if (matrix == null || matrix.length == 0) return false;
        int rows = matrix.length, cols = matrix[0].length;
        int start = 0, end = rows * cols - 1;
        while (start <= end){
            int mid = start + (end - start)/ 2;
            int value = matrix[mid / cols][mid % cols];
            if(value == target) return true;
            else if(value < target) start = mid + 1;
            else end = mid - 1;
        }
        return false;
    }
}
```

### Additional {#additional}




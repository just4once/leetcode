### Question {#question}

[https://leetcode.com/problems/rotate-image/description/](https://leetcode.com/problems/rotate-image/description/)

You are given annxn2D matrix representing an image.

Rotate the image by 90 degrees \(clockwise\).

**Note:**  
You have to rotate the image **in-place**, which means you have to modify the input 2D matrix directly.**DO NOT **allocate another 2D matrix and do the rotation.

**Example 1:**

```
Given input matrix = 
[
  [1,2,3],
  [4,5,6],
  [7,8,9]
],

rotate the input matrix in-place such that it becomes:
[
  [7,4,1],
  [8,5,2],
  [9,6,3]
]
```

**Example 2:**

```
Given input matrix =
[
  [ 5, 1, 9,11],
  [ 2, 4, 8,10],
  [13, 3, 6, 7],
  [15,14,12,16]
], 

rotate the input matrix in-place such that it becomes:
[
  [15,13, 2, 5],
  [14, 3, 4, 1],
  [12, 6, 8, 9],
  [16, 7,10,11]
]
```

### Thought Process {#thought-process}

1. Follow the requirement, and swap one element at the time
   1. Take the top left corner element put it in right top, then right top to bottom right, then bottom left
   2. Then we proceed to the next element
   3. We do this layer by layer until we reach to the core
2. Trick
   1. Flip upside down \(flip across the middle\)
   2. Flip diagonally from top left to bottom right

### Solution

```java
class Solution {
    public void rotate(int[][] matrix) {
        int n = matrix.length;
        // we start from layer 0, and going inward
        for (int l = 0; l < n / 2; l++) {
            for (int c = l; c < n - 1 - l; c++) {
                int tmp = matrix[l][c];
                matrix[l][c] = matrix[n - 1 - c][l];
                matrix[n - 1 - c][l] = matrix[n - 1 - l][n - 1 - c];
                matrix[n - 1 - l][n - 1 - c] = matrix[c][n - 1 - l];
                matrix[c][n - 1 - l] = tmp;
            }
        }
    }
}
```

```java
class Solution {
    public void rotate(int[][] matrix) {
        int n = matrix.length;
        int tmp = 0;
        int[] tmpA = null;
        //Flip up and down, horizontal accross the middle line
        for(int i =0; i < n/2; i++){
            tmpA = matrix[i];
            matrix[i] = matrix[n-i-1];
            matrix[n-i-1] = tmpA;
        }
        //Flip diagonally from top left to bottom right
        for(int i = 0; i < n; i++){
            for(int j = i + 1; j < n; j++){
                tmp = matrix[i][j];
                matrix[i][j] = matrix[j][i];
                matrix[j][i] = tmp;
            }
        }
    }
}
```

### Additional {#additional}




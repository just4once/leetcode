### Question {#question}

Given two [sparse matrices](https://en.wikipedia.org/wiki/Sparse_matrix) **A **and **B**, return the result of **AB**.

You may assume that **A**'s column number is equal to **B**'s row number.

**Example:**

```
A = [
  [ 1, 0, 0],
  [-1, 0, 3]
]

B = [
  [ 7, 0, 0 ],
  [ 0, 0, 0 ],
  [ 0, 0, 1 ]
]


     |  1 0 0 |   | 7 0 0 |   |  7 0 0 |
AB = | -1 0 3 | x | 0 0 0 | = | -7 0 3 |
                  | 0 0 1 |
```

### Thought Process {#thought-process}

1. Dot Product \(TLE\)
   1. Follow the rule of dot product
   2. Time complexity O\(mno\), where m = rows of A, n = columns of A, o = columns of B
   3. Space complexity O\(mo\)
2. Skip Value
   1. Instead of loop the rows of A and columns of B, we should loop through all the elements in the A then columns of B
   2. If the value of at particular i and j index is 0, we can skip jth row in B all together to save the work
   3. Time complexity O\(mno\), depends on the density of the graph
   4. Space complexity O\(mo\)

### Solution

```java
class Solution {
    public int[][] multiply(int[][] A, int[][] B) {
        if (A.length == 0 || B.length == 0) return new int[0][0];
        int m = A.length, n = A[0].length, o = B[0].length;
        int[][] res = new int[m][o];
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < o; j++) {
                for (int k = 0; k < n; k++) {
                    res[i][j] += A[i][k] * B[k][j];
                }
            }
        }
        return res;
    }
}
```

```java
class Solution {
    public int[][] multiply(int[][] A, int[][] B) {
        if (A.length == 0 || B.length == 0) return new int[0][0];
        int m = A.length, n = A[0].length, o = B[0].length;
        int[][] res = new int[m][o];
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                // if the value is not 0, it countribute to the sum
                if (A[i][j] != 0) {
                    for (int k = 0; k < o; k++) {
                        if (B[j][k] != 0) res[i][k] += A[i][j] * B[j][k];
                    }
                }
            }
        }
        return res;
    }
}
```

### Additional {#additional}




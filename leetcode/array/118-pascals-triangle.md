### Question {#question}

[https://leetcode.com/problems/pascals-triangle/description/](https://leetcode.com/problems/pascals-triangle/description/)

Given numRows, generate the first numRows of Pascal's triangle.

**Example:**

```
For example, given numRows = 5,
Return

[
     [1],
    [1,1],
   [1,2,1],
  [1,3,3,1],
 [1,4,6,4,1]
]
```

### Thought Process {#thought-process}

1. Each row in Pascal's triangle can be determined from previous row
2. For each column in the row, we can obtain the value by adding  pascal\[i - 1\]\[j - 1\] and pascal\[i -1\]\[j\], where i denotes the ith row, and j denotes the jth column
3. Time complexity O\(n^2\) because summing from 1 to n -&gt; n\(n +1\)/2
4. Space complexity O\(n^2\)

### Solution

```java
class Solution {
    public List<List<Integer>> generate(int numRows) {
        int[][] pascal = new int[numRows][];
        for (int i = 0; i < numRows; i++){
            int[] row = new int[i + 1];
            row[0] = 1;
            row[i] = 1;
            for (int j = 1; j < i; j++){
                row[j] = pascal[i - 1][j - 1] + pascal[i - 1][j];
            }
            pascal[i] = row;
        }
        return (List)Arrays.asList(pascal);
    }
}
```

### Additional {#additional}




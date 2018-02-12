### Question {#question}

Given a triangle, find the minimum path sum from top to bottom. Each step you may move to adjacent numbers on the row below.

For example, given the following triangle

**Example:**

```
[
     [2],
    [3,4],
   [6,5,7],
  [4,1,8,3]
]

The minimum path sum from top to bottom is 11 (i.e., 2 + 3 + 5 + 1 = 11).
```

### Thought Process {#thought-process}

1. The triangle is very similar to a tree structure, where at each node, we can either travel left or right
2. However, there is overlap of the subproblem, where the siblings share same leaf node, i.e. the left sibling and right sibling share their right leaf and left leaf respectively
3. From above observation, we can cache the result for each node
4. The best route sum can be calculate from backward, where sum\[i\]\[j\] equals math.min\(sum\[i + 1\]\[j\], sum\[i + 1\]\[j + 1\]\) + value\[i\]\[j\]
5. We can reduce the space usage to one dimensional array, since current sum depends on the row below
6. Time complexity O\(n^2\), where n is number of rows
7. Space complexity O\(n\)

### Solution

```java
class Solution {
    public int minimumTotal(List<List<Integer>> triangle) {
        int n = triangle.size();
        int[] dp = new int[n + 1];
        for (int i = n - 1; i >= 0; i--) {
            for (int j = 0; j <= i; j++) {
                dp[j] = Math.min(dp[j], dp[j + 1]) + triangle.get(i).get(j);
            }
        }
        return dp[0];
    }
}
```

### Additional {#additional}




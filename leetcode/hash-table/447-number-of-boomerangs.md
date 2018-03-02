### Question {#question}

Given n points in the plane that are all pairwise distinct, a "boomerang" is a tuple of points \(i, j, k\) such that the distance between i and j equals the distance between i and k \(the order of the tuple matters\).

Find the number of boomerangs. You may assume that n will be at most 500 and coordinates of points are all in the range \[-10000, 10000\] \(inclusive\).

**Example:**

```
Input:
[[0,0],[1,0],[2,0]]

Output:
2

Explanation:
The two boomerangs are [[1,0],[0,0],[2,0]] and [[1,0],[2,0],[0,0]]
```

### Thought Process {#thought-process}

1. Hash Table
   1. Use map to record the count of point that are equidistance to current point
   2. To calculate the count, we simply use the recorded count times count - 1, based on the permutation formula, nPk
   3. Time complexity O\(n^2\)
   4. Space complexity O\(n\)

### Solution

```java
class Solution {
    public int numberOfBoomerangs(int[][] points) {
        int res = 0;
        Map<Integer, Integer> map = new HashMap<>();
        for (int i = 0; i < points.length; i++) {
            for (int j = 0; j < points.length; j++) {
                if (i == j) continue;
                int d = distance(points[i], points[j]);
                map.put(d, map.getOrDefault(d, 0) + 1);
            }
            for (int val : map.values()) {
                res += val * (val - 1);
            }
            map.clear();
        }
        return res;
    }
    
    private int distance(int[] p, int[] q) {
        int dx = p[0] - q[0];
        int dy = p[1] - q[1];
        return dx * dx + dy * dy;
    }
}
```

### Additional {#additional}




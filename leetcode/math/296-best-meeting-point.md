### Question {#question}

[https://leetcode.com/problems/best-meeting-point/description/](https://leetcode.com/problems/best-meeting-point/description/)

A group of two or more people wants to meet and minimize the total travel distance. You are given a 2D grid of values 0 or 1, where each 1 marks the home of someone in the group. The distance is calculated using [Manhattan Distance](http://en.wikipedia.org/wiki/Taxicab_geometry), where distance\(p1, p2\) = \|p2.x - p1.x\| + \|p2.y - p1.y\|.

**Example:**

```
given three people living at (0,0), (0,4), and (2,2):

1 - 0 - 0 - 0 - 1
|   |   |   |   |
0 - 0 - 0 - 0 - 0
|   |   |   |   |
0 - 0 - 1 - 0 - 0

The point (0,2) is an ideal meeting point, as the total travel distance of 2+2+2=6 is minimal. So return 6.
```

### Thought Process {#thought-process}

1. Brute Force
   1. Try every point and calculate the 1's distance to this point
   2. The best distance can be found by using min function
   3. Time complexity O\(m^2n^2\)
   4. Space complexity O\(mn\)
2. Sorting
   1. The optimal point is at the mean
   2. For example, 1-1-0-0-1, the optimal point is at x = 1, and assume the total distance is d
   3. If we move the point to the right, x = 2, the total distance will be d +  2 - 1, since there will be two points on its left and 1 point on its right
   4. For even number of 1's, we can pick either one of middle as the choice, for example 1-1-0-0-1-1
   5. Time complexity O\(mn + mn log\(mn\)\) = O\(mn log\(mn\)\)
   6. Space complexity O\(mn\)
3. Without Sorting
   1. Write separate function for collecting rows and col
   2. Time complexity O\(mn\)
   3. Space complexity O\(mn\)
4. Two Pointers
   1. We can modify the distance function to use two pointers, using highIndex - lowIndex
   2. Time complexity O\(mn\)
   3. Space complexity O\(mn\)
5. One pass with Count
   1. We can modify the distance function to use frequency to find the reach the median
   2. Time complexity O\(mn\)
   3. Space complexity O\(mn\)

### Solution

```java
class Solution {
    public int minTotalDistance(int[][] grid) {
        if (grid.length == 0 || grid[0].length == 0) return 0;
        int min = Integer.MAX_VALUE;
        for (int i = 0; i < grid.length; i++) {
            for (int j = 0; j < grid[i].length; j++) {
                int dist = calculate(i, j, grid);
                min = Math.min(min, dist);
            }
        }
        return min;
    }

    private int calculate(int m, int n, int[][] grid) {
        int dist = 0;
        for (int i = 0; i < grid.length; i++) {
            for (int j = 0; j < grid[i].length; j++) {
                if (grid[i][j] == 1) dist += Math.abs(i - m) + Math.abs(n - j);
            }
        }
        return dist;
    }
}
```

```java
class Solution {
    public int minTotalDistance(int[][] grid) {
        if (grid.length == 0 || grid[0].length == 0) return 0;
        List<Integer> rows = new ArrayList<>();
        List<Integer> cols = new ArrayList<>();
        for (int i = 0; i < grid.length; i++) {
            for (int j = 0; j < grid[i].length; j++) {
                if (grid[i][j] == 1) {
                    rows.add(i);
                    cols.add(j);
                }
            }
        }
        Collections.sort(cols);
        return calDist(rows) + calDist(cols);
    }

    private int calDist(List<Integer> list) {
        int ref = list.get(list.size() / 2);
        int dist = 0;
        for (int point : list) {
            dist += Math.abs(point - ref);
        }
        return dist;
    }
}
```

```java
class Solution {
    public int minTotalDistance(int[][] grid) {
        if (grid.length == 0 || grid[0].length == 0) return 0;
        List<Integer> rows = collectRow(grid);
        List<Integer> cols = collectCol(grid);
        return calDist(rows) + calDist(cols);
    }

    private List<Integer> collectRow(int[][] grid) {
        List<Integer> res = new ArrayList<>();
        for (int i = 0; i < grid.length; i++) {
            for (int j = 0; j < grid[i].length; j++) {
                if (grid[i][j] == 1) {
                    res.add(i);
                }
            }
        }
        return res;
    }

    private List<Integer> collectCol(int[][] grid) {
        List<Integer> res = new ArrayList<>();
        for (int i = 0; i < grid[0].length; i++) {
            for (int j = 0; j < grid.length; j++) {
                if (grid[j][i] == 1) {
                    res.add(i);
                }
            }
        }
        return res;
    }

    private int calDist(List<Integer> list) {
        int ref = list.get(list.size() / 2);
        int dist = 0;
        for (int point : list) {
            dist += Math.abs(point - ref);
        }
        return dist;
    }
}
```

```java
class Solution {
    public int minTotalDistance(int[][] grid) {
        if (grid.length == 0 || grid[0].length == 0) return 0;
        List<Integer> rows = collectRow(grid);
        List<Integer> cols = collectCol(grid);
        return calDist(rows) + calDist(cols);
    }

    private List<Integer> collectRow(int[][] grid) {
        List<Integer> res = new ArrayList<>();
        for (int i = 0; i < grid.length; i++) {
            for (int j = 0; j < grid[i].length; j++) {
                if (grid[i][j] == 1) {
                    res.add(i);
                }
            }
        }
        return res;
    }

    private List<Integer> collectCol(int[][] grid) {
        List<Integer> res = new ArrayList<>();
        for (int i = 0; i < grid[0].length; i++) {
            for (int j = 0; j < grid.length; j++) {
                if (grid[j][i] == 1) {
                    res.add(i);
                }
            }
        }
        return res;
    }

    private int calDist(List<Integer> list) {
        int i = 0, j = list.size() - 1;
        int dist = 0;
        while (i < j) {
            dist += list.get(j) - list.get(i);
            i++;
            j--;
        }
        return dist;
    }
}
```

```java
class Solution {
    public int minTotalDistance(int[][] grid) {
        if (grid.length == 0 || grid[0].length == 0) return 0;
        int[] rowCount = new int[grid.length];
        int[] colCount = new int[grid[0].length];
        for (int i = 0; i < grid.length; i++) {
            for (int j = 0; j < grid[i].length; j++) {
                if (grid[i][j] == 1) {
                    rowCount[i]++;
                    colCount[j]++;
                }
            }
        }
        return calDist(rowCount) + calDist(colCount);
    }

    private int calDist(int[] count) {
        int i = 0, j = count.length - 1;
        int dist = 0;
        while (i < j) {
            int k = Math.min(count[i], count[j]);
            dist += k * (j - i);
            count[i] -= k;
            count[j] -= k;
            if (count[i] == 0) i++;
            if (count[j] == 0) j--;
        }
        return dist;
    }
}
```

### Additional {#additional}




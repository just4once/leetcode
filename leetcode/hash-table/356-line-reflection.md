### Question {#question}

[https://leetcode.com/problems/line-reflection/description/](https://leetcode.com/problems/line-reflection/description/)

Given n points on a 2D plane, find if there is such a line parallel to y-axis that reflect the given points.

**Example:**

```
Given points = [[1,1],[-1,1]], return true.
Given points = [[1,1],[-1,-1]], return false.
```

### Thought Process {#thought-process}

1. Hash Table - Two pass
   1. The reflection line has to be in the middle, meaning xref = \(xmin + xmax\) / 2
   2. Then we search if the there is reflected counterpart by searching point \[\(xmin + xmax\) - x, y\]
   3. Time complexity O\(n\)
   4. Space complexity O\(n\)

### Solution

```java
class Solution {
    public boolean isReflected(int[][] points) {
        int xMin = Integer.MAX_VALUE, xMax = Integer.MIN_VALUE;
        Set<String> set = new HashSet<>();
        for (int[] point : points) {
            xMin = Math.min(xMin, point[0]);
            xMax = Math.max(xMax, point[0]);
            set.add(point[0] + "," + point[1]);
        }
        int xSum = xMin + xMax;
        for (int[] point : points) {
            if (!set.contains((xSum - point[0]) + "," + point[1])) return false;
        }
        return true;
    }
}
```

```java
class Solution {
    public boolean isReflected(int[][] points) {
        int xMin = Integer.MAX_VALUE, xMax = Integer.MIN_VALUE;
        Set<Integer> set = new HashSet<>();
        for (int[] point : points) {
            xMin = Math.min(xMin, point[0]);
            xMax = Math.max(xMax, point[0]);
            set.add(Arrays.hashCode(point));
        }
        int xSum = xMin + xMax;
        for (int[] point : points) {
            int[] pRef = {xSum - point[0], point[1]};
            if (!set.contains(Arrays.hashCode(pRef))) return false;
        }
        return true;
    }
}
```

### Additional {#additional}




### Question {#question}

[https://leetcode.com/problems/max-points-on-a-line/description/](https://leetcode.com/problems/max-points-on-a-line/description/)

Given n points on a 2D plane, find the maximum number of points that lie on the same straight line.

**Example:**

```

```

### Thought Process {#thought-process}

1. Brute Force - HashMap
   1. We simply create all possible pair of points, and calculate their slope and intercept
   2. Use the string representation of slope
   3. Time complexity O\(n^2\)
   4. Space complexity O\(n^2\)

### Solution

```java
/**
 * Definition for a point.
 * class Point {
 *     int x;
 *     int y;
 *     Point() { x = 0; y = 0; }
 *     Point(int a, int b) { x = a; y = b; }
 * }
 */
class Solution {
    public int maxPoints(Point[] points) {
        if (points.length <= 2) return points.length;
        int n = points.length;
        int res = 0;
        for (int i = 0; i < n - 1; i++) {
            int sameP = 0, max = 0;
            Map<String, Integer> map = new HashMap<>();
            for (int j = i + 1; j < n; j++) {
                int x = points[i].x - points[j].x;
                int y = points[i].y - points[j].y;
                if (x == 0 && y == 0) {
                    sameP++;
                    continue;
                }
                // divide by gcd to reduce the factor in slope
                int gcd = gcd(x, y);
                x /= gcd;
                y /= gcd;
                String key = y + "/" + x;
                map.put(key, map.getOrDefault(key, 0) + 1);
                max = Math.max(max, map.get(key));
            }
            // +1 to include original point
            res = Math.max(res, max + sameP + 1);
        }
        return res;
    }

    private int gcd(int x, int y) {
        if (y == 0) return x;
        return gcd(y, x % y);
    }
}
```

### Additional {#additional}




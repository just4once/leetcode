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

### Solution

```java

```

### Additional {#additional}




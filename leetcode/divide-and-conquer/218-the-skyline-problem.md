# 218-the-skyline-problem

## Question {#question}

[https://leetcode.com/problems/the-skyline-problem/description/](https://leetcode.com/problems/the-skyline-problem/description/)

A city's skyline is the outer contour of the silhouette formed by all the buildings in that city when viewed from a distance. Now suppose you are **given the locations and height of all the buildings** as shown on a cityscape photo \(Figure A\), write a program to **output the skyline** formed by these buildings collectively \(Figure B\).[![Buildings](https://leetcode.com/static/images/problemset/skyline1.jpg) ](https://leetcode.com/static/images/problemset/skyline1.jpg)[![Skyline Contour](https://leetcode.com/static/images/problemset/skyline2.jpg)](https://leetcode.com/static/images/problemset/skyline2.jpg)

The geometric information of each building is represented by a triplet of integers `[Li, Ri, Hi]`, where `Li` and `Ri` are the x coordinates of the left and right edge of the ith building, respectively, and `Hi` is its height. It is guaranteed that `0 ≤ Li, Ri ≤ INT_MAX`, `0 < Hi ≤ INT_MAX`, and `Ri - Li > 0`. You may assume all buildings are perfect rectangles grounded on an absolutely flat surface at height 0.

For instance, the dimensions of all buildings in Figure A are recorded as: `[ [2 9 10], [3 7 15], [5 12 12], [15 20 10], [19 24 8] ]` .

The output is a list of "**key points**" \(red dots in Figure B\) in the format of `[ [x1,y1], [x2, y2], [x3, y3], ... ]` that uniquely defines a skyline. **A key point is the left endpoint of a horizontal line segment**. Note that the last key point, where the rightmost building ends, is merely used to mark the termination of the skyline, and always has zero height. Also, the ground in between any two adjacent buildings should be considered part of the skyline contour.

For instance, the skyline in Figure B should be represented as:`[ [2 10], [3 15], [7 12], [12 0], [15 10], [20 8], [24, 0] ]`.

**Notes:**

* The number of buildings in any input list is guaranteed to be in the range `[0, 10000]`.
* The input list is already sorted in ascending order by the left x position `Li`.
* The output list must be sorted by the x position.
* There must be no consecutive horizontal lines of equal height in the output skyline. For instance, `[...[2 3], [4 5], [7 5], [11 5], [12 7]...]` is not acceptable; the three lines of height 5 should be merged into one in the final output as such: `[...[2 3], [4 5], [12 7], ...]`

## Thought Process {#thought-process}

1. PriorityQueue
   1. To get the outline of the buildings, we need to go through all the critical points in the chart and check whether we add them base on followings
   2. One particular useful data structure to get max or min in log\(n\) times is heap, so we are going to use heap to retrieve max height efficiently
   3. We use a list save all the critical points and sort them
      1. First based on the left coordinate
      2. Second reverse in height, because if the left coordinate is the same, we should use the taller height in outline
   4. If the current critical point is a starting point, and we find the currentMaxH != prevH, we can add it to our outlines
   5. If the current critical point is a ending point, we need to remove its starting point from our heap, and also compare currentMaxH to prevH, if they are different, we can add it to out outline, otherwise it's shadowed
   6. Time complexity O\(n^2\), n from all the points and n from remove it from hepa
   7. Space complexity O\(n\)
2. TreeMap
   1. To avoid O\(n\) time in removing object, we can use treemap instead to mark the entry where the entry's key is height and value is count
   2. We continues decrease the count when we hit the right point and remove when the count = 1
   3. Time complexity O\(nlogn\)
   4. Space complexity O\(n\)
3. Divide and Conquer
   1. We can separate the list into two equal parts, where we find the skyline for left and right and then we merge
   2. Merging part is little bit tricky where we have to keep the height of each side
   3. When comparing left and right skyline, we can poll the minX point out and then check its height with current height

## Solution

PriorityQueue

```java
class Solution {
    private class Point implements Comparable<Point> {
        int x, y;
        boolean isLeft;
        
        public Point(int x, int y) {
            this(x, y, false);
        }
        
        public Point(int x, int y, boolean isLeft) {
            this.x = x;
            this.y = y;
            this.isLeft = isLeft;
        }
        
        public int compareTo(Point that) {
            return this.x == that.x ? that.y - this.y : this.x - that.x;
        }
    }
    
    public List<int[]> getSkyline(int[][] buildings) {
        // identify all the critical points
        List<Point> points = new ArrayList<>();
        for (int[] building : buildings) {
            points.add(new Point(building[0], building[2], true));
            points.add(new Point(building[1], building[2]));
        }
        Collections.sort(points);
        PriorityQueue<Integer> maxHeap = new PriorityQueue<>((a, b) -> b - a);
        maxHeap.offer(0);
        int preH = 0;
        List<int[]> res = new ArrayList<>();
        for (Point point : points) {
            if (point.isLeft) maxHeap.offer(point.y);
            else maxHeap.remove(point.y);
            int curH = maxHeap.peek();
            if (curH != preH) {
                res.add(new int[]{point.x, curH});
                preH = curH;
            }
        }
        return res;
    }
}
```

```java
class Solution {    
    public List<int[]> getSkyline(int[][] buildings) {
        // identify all the critical points
        List<int[]> points = new ArrayList<>();
        for (int[] building : buildings) {
            points.add(new int[]{building[0], -building[2]});
            points.add(new int[]{building[1], building[2]});
        }
        Collections.sort(points, (a, b) -> a[0] == b[0] ? a[1] - b[1] : a[0] - b[0]);
        PriorityQueue<Integer> maxHeap = new PriorityQueue<>((a, b) -> b - a);
        maxHeap.offer(0);
        int preH = 0;
        List<int[]> res = new ArrayList<>();
        for (int[] point : points) {
            if (point[1] < 0) maxHeap.offer(-point[1]);
            else maxHeap.remove(point[1]);
            int curH = maxHeap.peek();
            if (curH != preH) {
                res.add(new int[]{point[0], curH});
                preH = curH;
            }
        }
        return res;
    }
}
```

2. PriorityQueue with TreeMap

```java
class Solution {    
    public List<int[]> getSkyline(int[][] buildings) {
        // identify all the critical points
        List<int[]> points = new ArrayList<>();
        for (int[] building : buildings) {
            points.add(new int[]{building[0], -building[2]});
            points.add(new int[]{building[1], building[2]});
        }
        // sort it base on the left point else by the reverse height
        Collections.sort(points, (a, b) -> a[0] == b[0] ? a[1] - b[1] : a[0] - b[0]);
        // use treemap can avoid the O(n) time cost on heap, we can remove
        // the item when height count = 1
        TreeMap<Integer, Integer> treeMap = new TreeMap<>(Collections.reverseOrder());
        treeMap.put(0, 1);
        int preH = 0;
        List<int[]> res = new ArrayList<>();
        // For every point, we need to get the maxCurH to compare to preH
        // If there are different, this means we can add the point to the
        // outline
        for (int[] point : points) {
            if (point[1] < 0) treeMap.put(-point[1], treeMap.getOrDefault(-point[1], 0) + 1);
            else if (treeMap.get(point[1]) == 1) treeMap.remove(point[1]);
            else treeMap.put(point[1], treeMap.get(point[1]) - 1);
            int curH = treeMap.firstKey();
            if (curH != preH) {
                res.add(new int[]{point[0], curH});
                preH = curH;
            }
        }
        return res;
    }
}
```

3. Divide and Conquer

```java
class Solution {    
    public List<int[]> getSkyline(int[][] buildings) {
        // we can use divide and conquer approach as well
        if (buildings.length == 0) return new LinkedList<int[]>();
        return search(buildings, 0, buildings.length - 1);
    }
    
    private LinkedList<int[]> search(int[][] buildings, int lo, int hi) {
        if (lo < hi) {
            int mi = lo + (hi - lo) / 2;
            return merge(search(buildings, lo, mi), search(buildings, mi + 1, hi));
        } else {
            LinkedList<int[]> res = new LinkedList<>();
            res.add(new int[]{buildings[lo][0], buildings[lo][2]});
            res.add(new int[]{buildings[lo][1], 0});
            return res;
        } 
    }
    
    private LinkedList<int[]> merge(LinkedList<int[]> left, LinkedList<int[]> right) {
        LinkedList<int[]> res = new LinkedList<>();
        int h1 = 0, h2 = 0;
        // Merging is little bit tricky, we need two separate variables to
        // Check the height add appropiately two shadowed buildings
        
        // h1 and h2 each track the building height on left and right respectively
        // Now when a shadowed building comes in, our h will guard and prevent the
        // building being added.
        while (!left.isEmpty() && !right.isEmpty()) {
            int x = 0, h = 0;
            if (left.peek()[0] < right.peek()[0]) {
                x = left.peek()[0];
                h1 = left.poll()[1];
            } else if (right.peek()[0] < left.peek()[0]) {
                x = right.peek()[0];
                h2 = right.poll()[1];
            } else {
                x = left.peek()[0];
                h1 = left.poll()[1];
                h2 = right.poll()[1];
            }
            h = Math.max(h1, h2);
            if (res.isEmpty() || h != res.getLast()[1]) res.add(new int[]{x, h});
        }
        res.addAll(left);
        res.addAll(right);
        return res;
    }
}
```

## Additional {#additional}


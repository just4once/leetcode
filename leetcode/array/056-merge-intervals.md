### Question {#question}

[https://leetcode.com/problems/merge-intervals/description/](https://leetcode.com/problems/merge-intervals/description/)

Given a collection of intervals, merge all overlapping intervals.

**Example:**

```
Given [1,3],[2,6],[8,10],[15,18],
return [1,6],[8,10],[15,18]
```

### Thought Process {#thought-process}

1. Brute Force
   1. We can check current interval against previously inserted intervals for interval overlaping
   2. Time complexity O\(n^2\)
   3. Space complexity O\(n\), extra space O\(1\)
2. Sort By the end
   1. To merge intervals more efficiently, we have to group them more closely
   2. By assuming the end of intervals are greater than or equal to their start, we can sort all the intervals by their start
   3. Now, we save an interval as a reference called prev, then we check if there is overlap
      1. No overlap when the start of new interval is greater than its end, then we can add prev to our result
      2. Otherwise, we need to expand our prev
   4. Time complexity O\(n log n\)
   5. Space complexity O\(n\), extra space depends on it we allowed to sort on the original list

### Solution

```java
/**
 * Definition for an interval.
 * public class Interval {
 *     int start;
 *     int end;
 *     Interval() { start = 0; end = 0; }
 *     Interval(int s, int e) { start = s; end = e; }
 * }
 */
class Solution {
    public List<Interval> merge(List<Interval> intervals) {
        LinkedList<Interval> result = new LinkedList<>();
        if (intervals == null || intervals.size() == 0) return result;
        Collections.sort(intervals, (a, b) -> a.start - b.start);
        Interval cur = intervals.get(0);
        result.add(new Interval(cur.start, cur.end));
        for (int i = 1; i < intervals.size(); i++) {
            cur = intervals.get(i);
            if (cur.start > result.getLast().end) {
                result.add(new Interval(cur.start, cur.end));
            } else {
                Interval prev = result.getLast();
                prev.end = Math.max(prev.end, cur.end);
            }
        }
        return result;
    }
}
```

```java
class Solution {
    public List<Interval> merge(List<Interval> intervals) {
        List<Interval> result = new ArrayList<>();
        if (intervals == null || intervals.size() == 0) return result;
        int n = intervals.size();
        int[] start = new int[n];
        int[] end = new int[n];
        for (int i = 0; i < n; i++) {
            start[i] = intervals.get(i).start;
            end[i] = intervals.get(i).end;
        }
        Arrays.sort(start);
        Arrays.sort(end);
        // we have array of start and end, and two pointers
        // [1,3],[2,6],[8,10],[15,18]
        // start: 1 2 8  15
        // end:   3 6 10 18
        // j keep track of the start
        for (int i = 0, j = 0; i < n; i++) {
            if (i == n - 1 || start[i + 1] > end[i]) {
                result.add(new Interval(start[j], end[i]));
                j = i + 1;
            }
        }
        return result;
    }
}
```

### Additional {#additional}




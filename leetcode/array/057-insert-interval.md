# 057-insert-interval

## Question {#question}

[https://leetcode.com/problems/insert-interval/description/](https://leetcode.com/problems/insert-interval/description/)

Given a set ofnon-overlappingintervals, insert a new interval into the intervals \(merge if necessary\).

You may assume that the intervals were initially sorted according to their start times.

**Example 1:**

```text
Given intervals [1,3],[6,9], insert and merge [2,5] in as [1,5],[6,9].
```

**Example 2:**

```text
Given [1,2],[3,5],[6,7],[8,10],[12,16], insert and merge [4,9] in as [1,2],[3,10],[12,16].

This is because the new interval [4,9] overlaps with [3,5],[6,7],[8,10].
```

## Thought Process {#thought-process}

1. Since the input it's sorted, we can easily compare our merge interval overlap with our exploring interval
2. If there is no overlap between this interval and the merge interval, we can just add it to the result list
3. If there is overlap, we can start merge the intervals until there is no overlap
4. Add the remaining intervals
5. Time complexity O\(n\)
6. Space complexity O\(n\), O\(1\) extra

## Solution

```java
class Solution {
    public List<Interval> insert(List<Interval> intervals, Interval newInterval) {
        List<Interval> res = new ArrayList<>();
        int n = intervals.size();
        int i = 0;
        Interval cur = null;
        while (i < n && newInterval.start > intervals.get(i).end) {
            cur = intervals.get(i);
            res.add(new Interval(cur.start, cur.end));
            i++;
        }
        cur = new Interval(newInterval.start, newInterval.end);
        while (i < n && intervals.get(i).start <= cur.end) {
            cur.start = Math.min(cur.start, intervals.get(i).start);
            cur.end = Math.max(cur.end, intervals.get(i).end);
            i++;
        }
        res.add(cur);
        while (i < n) {
            cur = intervals.get(i);
            res.add(new Interval(cur.start, cur.end));
            i++;
        }
        return res;
    }
}
```

## Additional {#additional}


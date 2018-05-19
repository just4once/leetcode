### Question {#question}

[https://leetcode.com/problems/find-right-interval/description/](https://leetcode.com/problems/find-right-interval/description/)

Given a set of intervals, for each of the interval i, check if there exists an interval j whose start point is bigger than or equal to the end point of the interval i, which can be called that j is on the "right" of i.

For any interval i, you need to store the minimum interval j's index, which means that the interval j has the minimum start point to build the "right" relationship for interval i. If the interval j doesn't exist, store -1 for the interval i. Finally, you need output the stored value of each interval as an array.

**Note:**

1. You may assume the interval's end point is always bigger than its start point.
2. You may assume none of these intervals have the same start point.

**Example 1:**

```
Input: [ [1,2] ]

Output: [-1]

Explanation: There is only one interval in the collection, so it outputs -1.
```

**Example 2:**

```
Input: [ [3,4], [2,3], [1,2] ]

Output: [-1, 0, 1]

Explanation: There is no satisfied "right" interval for [3,4].
For [2,3], the interval [3,4] has minimum-"right" start point;
For [1,2], the interval [2,3] has minimum-"right" start point.
```

**Example 3:**

```
Input: [ [1,4], [2,3], [3,4] ]

Output: [-1, 2, -1]

Explanation: There is no satisfied "right" interval for [1,4] and [3,4].
For [2,3], the interval [3,4] has minimum-"right" start point.
```

### Thought Process {#thought-process}

1. Brute Force
   1. Simply find the minimum index that has start greater than current end
   2. As we loop we need to find the start that is smaller than previous found start
   3. Time complexity O\(n^2\)
   4. Space complexity O\(1\) extra, O\(n\) for storing result
2. Sort and Binary Search
   1. Save the position for each starts in map
   2. Create a separate to store the starts and sort them
   3. As we loop through the intervals array, we try to search the end in the starts array create in step ii
   4. If the return index, j, is equal to length that means we could not find a start pointer bigger than the end
   5. Otherwise, we need to get the index for starts\[j\] from our map and save it to out result array, res\[i\]
   6. Time complexity O\(nlogn\)
   7. Space complexity O\(n\)
3. TreeMap
   1. Using treemap to store the entry, where entry's key is the interval's start and the value is the index, we can find each interval's end ceiling interval easily with built-in function
   2. Time complexity O\(nlogn\)
   3. Space complexity O\(n\)
4. Sorted Both and Linear Scan
   1. Time complexity O\(nlogn\)
   2. Space complexity O\(n\)
   3. 

### Solution

```java
public class Solution {
    public int[] findRightInterval(Interval[] intervals) {
        int[] res = new int[intervals.length];
        for (int i = 0; i < intervals.length; i++) {
            int min = Integer.MAX_VALUE;
            int minindex = -1;
            for (int j = 0; j < intervals.length; j++) {
                if (intervals[j].start >= intervals[i].end && intervals[j].start < min) {
                    min = intervals[j].start;
                    minindex = j;
                }
            }
            res[i] = minindex;
        }
        return res;
    }
}
```

```java
class Solution {
    public int[] findRightInterval(Interval[] intervals) {
        int n = intervals.length;
        int[] res = new int[n], starts = new int[n];
        Map<Integer, Integer> map = new HashMap<>();
        for (int i = 0; i < n; i++) {
            map.put(intervals[i].start, i);
            starts[i] = intervals[i].start;
        }
        Arrays.sort(starts);
        for (int i = 0; i < n; i++) {
            int j = binarySearch(starts, intervals[i].end, 0, n);
            res[i] = j == n ? -1 : map.get(starts[j]);
        }
        return res;
    }

    private int binarySearch(int[] nums, int target, int i, int j) {
        j--;
        while (i <= j) {
            int m = i + (j - i) / 2;
            if (nums[m] == target) return m;
            else if (nums[m] < target) i = m + 1;
            else j = m - 1;
        }
        return i;
    }
}
```

```java
class Solution {
    public int[] findRightInterval(Interval[] intervals) {
        TreeMap<Integer, Integer> treeMap = new TreeMap<>();
        int n = intervals.length;
        for (int i = 0; i < n; i++) {
            treeMap.put(intervals[i].start, i);
        }
        int[] res = new int [n];
        for (int i = 0; i < n; i++) {
            Map.Entry<Integer, Integer> entry = treeMap.ceilingEntry(intervals[i].end);
            res[i] = entry == null? -1 : entry.getValue();
        }
        return res;
    }
}
```

### Additional {#additional}




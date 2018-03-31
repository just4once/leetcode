### Question {#question}

[https://leetcode.com/problems/smallest-range/description/](https://leetcode.com/problems/smallest-range/description/)

You have **k** lists of sorted integers in ascending order. Find the **smallest** range that includes at least one number from each of the **k** lists.

We define the range \[a,b\] is smaller than range \[c,d\] if **b-a &lt; d-c** or **a &lt; c** if **b-a == d-c**.

**Example:**

```
Input:[[4,10,15,24,26], [0,9,12,20], [5,18,22,30]]
Output: [20,24]
Explanation: 
List 1: [4, 10, 15, 24,26], 24 is in range [20,24].
List 2: [0, 9, 12, 20], 20 is in range [20,24].
List 3: [5, 18, 22, 30], 22 is in range [20,24].
```

1. The given list may contain duplicates, so ascending order means &gt;= here.
2. 1 &lt;= k &lt;= 3500
3. -105 &lt;= value of elements &lt;= 105.

### Thought Process {#thought-process}

1. Brute Force
   1. Time complexity O\(n^3\)
   2. Space complexity o\(1\)
2. Pointers \(TLE\)
   1. Use next\[i\] to store the number to be consider next for each ith list
   2. For the first time, we are considering the min of all the list
   3. If we get the min and max for the current considerations \(where the next\[i\] pointers point to\), we have include 1 number from each list
   4. To make the range possible smaller, we can either decrease the max or increase the min. However, increasing the min is the only option because the other choice will exclude one of the list
   5. Time complexity O\(mn\), where m is number of rows, and n is total elements
   6. Space complexity O\(m\)
3. asd

### Solution

Pointers \(TLE\)

```java
class Solution {
    public int[] smallestRange(List<List<Integer>> nums) {
        int min = 0, max = Integer.MAX_VALUE;
        int[] next = new int[nums.size()];
        while (true) {
            int minRow = 0, maxRow = 0;
            for (int i = 0; i < next.length; i++) {
                if (nums.get(i).get(next[i]) < nums.get(minRow).get(next[minRow])) minRow = i;
                if (nums.get(i).get(next[i]) > nums.get(maxRow).get(next[maxRow])) maxRow = i;
            }
            if (max - min > nums.get(maxRow).get(next[maxRow]) - nums.get(minRow).get(next[minRow])) {
                max = nums.get(maxRow).get(next[maxRow]);
                min = nums.get(minRow).get(next[minRow]);
            }
            next[minRow]++;
            if (next[minRow] == nums.get(minRow).size()) break;
        }
        return new int[] {min, max};
    }
}
```

### Additional {#additional}



